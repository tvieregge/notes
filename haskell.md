#### Type class
Defines a protocol for using an object rather than defining an object itself.  
Ex. Eq type class defines the function

    (==) :: (Eq a) => a -> a -> Bool

#### Type constructor
Takes in types as parameters to produce new types.
Ex. The Maybe type has a single type parameter 'a' and is defined as

    data Maybe a = Nothing | Just a

#### Functor Laws

    fmap id = id
    fmap (f . g) = fmap f . fmap g

#### Data constructor
A function taking some values as its arguments, and then uses those to construct a  
new value.

    data Colour = RGB Int Int Int

RGB is a data constructor with type

    RGB :: Int -> Int -> Int -> Colour
