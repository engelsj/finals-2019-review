# Section A

1. Give a complete implementation of the Prelude functions described below. By "complete" is meant that any other functions used to help implement those below must also have their implementations given. 

a. Returns the first element of a list, if it is non-empty, with a runtime error otherwise.

```haskell
head :: [a] -> a -- Type Signature
head (x:_) = x -- Non-Empty List
head [] = error "Prelude.head: empty list" -- Empty List
```

b. Returns the last element of a list, if it is non-empty, with a runtime error otherwise

```haskell
last :: [a] -> a -- Type Signature
last [x] = x -- Singleton List -- must occur before (_:xs) clause
last(_:xs) = last xs -- Non-Empty List
last [] = error "Prelude.head empty list" -- Empty List
```

c. Concatenate two lists together

```haskell
(++) :: [a] -> [a] -> [a] -- Type Signature
[] ++ ys = ys -- Empty List -- Empty List
(x:xs) ++ ys = x : (xs ++ ys) -- Non-Empty List
```

d. Reverse its list argument

```haskell
reverse :: [a] -> [a] -- Type Signature 
reverse [] = [] -- Empty List
reverse (x:xs) = reverse xs ++ [x] -- Non-Empty List 
```

e. Use a predicate to split a list into two, the first list being the longest prefix that satifies the predicate, while the second list is what remains 

```haskell
span :: (a -> Bool) -> [a] -> ([a],[a])
span p [] = ([],[])
span p (x:xs) 
	| p x = let (before, after) = span p xs in (x:before, after)
	| otherwise = ([], x:xs)
```

f. Compute the minimum of a non-empty list

```haskell
minimum :: Ord a => [a] -> a -- Type Signature
minimum [] = error "Prelude.minimum Minimum of empty list" -- Empty List
minimum[x] = x -- Singleton List
minimum(x:xs) = min x (minimum xs) -- Non-Empty List

min[x] = x
min(x:xs)
	= if x < min xs
		then x
		else min xs 
```

2. We have a binary search tree built from number-string pairs, ordered by the number (acting as key)

   ```haskell
   data BinTree = BNil
   	| BOne Int String
   	| BTwo BinTree Int String BinTree
   ```

   and one function lookup partiall defined over it

   ```haskell
   lookup :: BinTree -> Int -> String 
   lookup (BOne i s) x 
   		| x == i = s
   
   lookup (Btwo left i s right) x
   		| x < i = lookup left x
   		| x > i = lookup right x
   ```

a. Describe the three ways in which function ```lookup``` can fail, with Haskell runtime pattern-matching errors.

Match the pattern but do not pass the guards where x != i 

No pattern that matches when the answer is within the Btwo tree 

b. Add in error handling for function ```lookup``` above, using the ```Maybe``` type, to ensure this function is now total. Note that this will require changing the type of the ```lookup``` function. Your answer should give the new type.

```haskell
lookup :: BinTree -> Int -> Maybe String
lookup Bnil i = Nothing
lookup (Bone i s) x
	| i == x Just s 
	| otherwise Nothing

lookup(Btwo left i s right) x
	| x < i = lookup left x
	| x > i = lookup right x
```

c. Add in generic error handling for the ```lookup``` function above, using monads, ensuring it is now total, and giving back a useful error message. Note that this will require changing the type (again) of the ```lookup``` function and your answer should give the revised type. 

```

```

