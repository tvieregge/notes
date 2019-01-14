#### Type class
Defines a protocol for using an object rather than defining an object itself.  
Ex. Eq type class defines the function

    (==) :: (Eq a) => a -> a -> Bool

#### Type constructor
Takes in types as parameters to produce new types.
Ex. The Maybe type has a single type parameter 'a' and is defined as

    data Maybe a = Nothing | Just a

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

__Applicative Functors:__ Functors that can be mapped over other functors. They implement
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

__Applicative Examples:__

    ((+) <$> (+3) <*> (*100)) === ((\x -> ((+) (3 + x))) <*> (*100))
    (:) <$> (+4) <*> pure [] ===
    (\x -> ((:) (4 + x))) <*> pure []) ===
    (\y -> (\x -> ((:) (4 + x))) y) y []

#### Monads
*TODO*
