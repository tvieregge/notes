#### Type class
Defines a protocol for using an object rather than defining an object itself.  
Ex. Eq type class defines the function

    (==) :: (Eq a) => a -> a -> Bool

#### Type constructor
Takes in types as parameters to produce new types.
Ex. The Maybe type has a single type parameter 'a' and is defined as

    data Maybe a = Nothing | Just a
