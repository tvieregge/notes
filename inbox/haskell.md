*It looks like this is generally a subset of "What I Wish I Knew When Learning Haskell"
located here: http://dev.stephendiehl.com/hask/ . I think the exercise of making
this is useful for me right now, but I'll likely stop soon and contribute anything new
I have to that document.*

#### Type class
Defines a protocol for using an object rather than defining an object itself.  
Ex. Eq type class defines the function

    (==) :: (Eq a) => a -> a -> Bool

#### Type constructor
Takes in types as parameters to produce new types.
Ex. The Maybe type has a single type parameter 'a' and is defined as

    data Maybe a = Nothing | Just a

Generally you do not add type class constraints in data decl.
It doesn't provide much because you would still need the constraint in functions
that take the type and also restricts functions that use the type but don't rely
on the constraint.

Its type signature is `toList :: Map k a -> [(k, a)]`. If `Map k v` had a type con-
straint in its data declaration, the type for `toList` would need to be `toList ::
(Ord k) => Map k a -> [(k, a)]`, even though the function doesn’t compare
keys by order.

#### Data constructor
A function taking some values as its arguments, and then uses those to construct a  
new value.

    data Colour = RGB Int Int Int

RGB is a data constructor with type

    RGB :: Int -> Int -> Int -> Colour


#### Computational Context
The context that functors give their values.

    data Mabey a = Nothing | Just a

This give *a* the context of Mabey, i.e. it could be nothing OR Just the value.  
Another way to think about it: |Mabey a| = 1 + |a|. This is because you can have a 'Just'
for any a, or a Nothing.

### Functors, Applicative Functors and Monads
__Functors:__ Things that can be mapped over by functions. They implement fmap which applies
the function *inside* the context of the functor.  

    fmap :: (a -> b) -> f a -> f b

__Ex.__  

    $ fmap (+3) [1,2,3]  
    [4,5,6]

fmap allows us to lift a function into that context. The fmap function can’t access
any information in the context, and it’s not allowed to change the context.  
More formally:

    fmap id = id
    fmap (f . g) = fmap f . fmap g

__Applicative Functors:__ Functors that can be mapped over other functors.
*[[error handling with applicative functors]] is a particularly good use*

They implement
*pure* which put the value in a default context (lifts the value) and *<\*>*, which applies
the function from *inside* the context of one functor to the value *inside* the context of
another.

    (<*>) :: (Applicative f) => f (a -> b) -> f a -> f b
    pure :: a -> f a

Have the abilit to use the *computational context*

    instance Applicative Maybe where
        pure = Just
        (Just f)  <*> m = fmap f m
        Nothing <*> _ = Nothing

The contextual application says “If any of these contexts is Nothing, then the whole
context is Nothing”. As another example, lists use the context of the length to create a
new, longer list.

Solve a problem: What if we want to map a function that takes two (or an number) params over
a functor?

    $ fmap (fmap (+) [1,2,3]) 4
    error
    $ (+) <$> [1,2,3] <*> pure 4
    [5,6,7]

__Applicative Law(s):__ There are a bunch, only this one seems to get any attention.

    pure f <*> a === fmap f a

__Applicative *functions*:__ The implementation of <*> is a bit tricky.

    (<*>) :: (Applicative f) => f (a -> b) -> f a -> f b
    f <*> g = \x -> f x (g x)

Specializing the type to `((->) r)` we have:

    Applicative ((->) r) => ((->) r) (a -> b) -> ((->) r) a -> ((->) r) b

Looking back at the definition of <*> we have

* f is a function that returns a function, and takes a parameter of type r
* g is a function that returns a value and takes a parameter of type r
* x is a value of type r

Because of curring `f x (g x)` does *not* mean f is given the result of (g x) as a
param, the function that f *returns* is. This leads to the following steps.

    f <*> g = \x -> f x (g x)
    \x -> f1 (g x)              -- f takes x and returns a function f1 :: a -> b
    \x -> f1 v                  -- g takes x and returnes v :: a
    \x -> f2                    -- f1 takes v, f2 :: b. The lambda makes it r -> b

See [this link](https://wjdhamilton.blogspot.com/2016/08/f-f-x-g-x.html) for more explanation.

__Applicative Examples:__

    Just (+2) <*> Just 5 === Just 7

    ((+) <$> (+3) <*> (*100)) ===
    ((\x -> ((+) (3 + x))) <*> (*100)) ===
    (\x -> ((+) (3 + x) (x*100))) ===

    (:) <$> (+4) <*> pure [] ===
    ((\x -> ((:) (4 + x))) <*> pure []) ===
    (\x -> ((:) (4 + x) []))

### Monoids
A class with an associative binary function, an identity value and a function to recude
a list to a value.

#### Monoid Laws

    mempty `mappend` x = x | <- identity
    x `mappend` mempty = x |
    (x `mappend` y) `mappend` z = x `mappend` (y `mappend` z) <- associative

#### Why they matter
The ability to combine components of type A into a single component of type a is useful,
reduces the layring of abstractions. Solves:

    Oh no, these Bs are not connectable, so let's make a network of Bs and call that a C.
    Well, I want to assemble several Cs, so let's make a network of Cs and call that a D

### Monads
Monads solve the problem of applying a value with a context (m a) to a function that take a
normal value and returned a context (a -> mb). They also support the return function which
puts a value in it's minimal context (like pure), >> which is like >>= with a default
function that ignores it's input and fail, which is called when pattern matching in a do
block fails (and maybe other times?).

Here is the implmentation of the list monad.

    return :: a -> m a
    return x = [x]

    (>>=) :: m a -> (a -> m b) -> m b
    xs >>= f = concat (map f xs)

    (>>) :: m a -> m b -> m b
    x >> y = x >>= \_ -> y

    fail :: String -> m a
    fail _ = []

A monad is a monoid object in a category of endofunctors: return is the unit, and
join is the binary operation.

#### Monad Laws
The language itself cannot check for these laws.

Left Identity: Putting a value in a default context, then binding it to a function
is the same as calling that function with the value.

    return x >>= f = f x

Right Identit: If we bind a monadic value to return we get the same monadic value back.
Basically return doesn't change the value or add any context.

    m >>= return = m

Associativity: it doesn't matter how monadic function application is nested. This is
awkward with the bind function.

    (m >> f) >>= g = m >>= (\x - f x >> g)

This is better with the monad composition operator the equivalent of (.)

    (<=<) :: (Monad m) => (b -> m c) -> (a -> m b) -> (a -> m c)
    f <=< g = (\x -> g x >>= f)

Now:

    (f >=> g) >=> h = f >=> (g >=> h)

This law allows following two things to be equivalent, which clearl should be correct

    main = do
            answer <- do
                            unused <- getLine
                            getLine
            putStrLn answer

    main = do
            unused <- getLine
            answer <- getLine
            putStrLn answer

#### Reader monad (functions as monads)

Simillar to functions as applicatives.

    (>>=) :: m a -> (a -> m b) -> m b
    (>>=) :: ((->) r) a -> (a -> ((->) r) b) -> ((->) r) b

    h >>= f = \w -> f (h w) w
    \w -> f h' w                -- h :: r -> a, => h' :: a
    \w -> f' w                  -- f :: a -> r -> b, => f' :: r -> b
    \w -> f''                   -- f'' :: b, so resulting lambda :: r -> b

This allows us to give a constant environment for evaluating functions (kind fo like a
global variable). When evaluating `(h >>= f) r = f (h r) r` we first evaluate h in the
context of r to get h', then evaluate then evaluate f of h' in the context of r.

Foldr - constructor replacement. Replace cons with the given function. Doesn't consume
list from the right!
Foldl - for loop

    foldr (+) 0 1:2:3:[] ->
        1+2:3+0

    foldl (+) 0 xs ->
        accum = 0
        for each x in xs
            accume += x
        return accume


