## Section A

1a. Returns the list with its first element removed, if it is non-empty, with a runtime error otherwise.

```haskell
tail :: [a] -> [a]
tail (_:xs) = xs
tail [] = error "Empty List"
```

1b. Concatenate two lists together 

```haskell
(++) :: [a] -> [a] -> [a]
[] ++ ys = ys
(x:xs) ++ ys = x :(xs ++ ys)
```

1c. Returns everything but the last element of a list, if it is non-empty, with a runtime error otherwise.

```Haskell
init :: [a] -> [a]
init [x] = []
init (x:xs) = x : init xs
init [] = error "Empty List"
```

1d. Reverse its list argument

```haskell
reverse :: [a] -> [a]
reverse [] = [] 
reverse (x:xs) = reverse xs ++ [x]

(++) :: [a] -> [a] -> [a]
[] ++ ys = ys
(x:xs) ++ ys = x :(xs ++ ys)
```

1e. Use a predicate to split a list into two, the first list being the longest prefix that does not satisfy the predicate, while the second list is what remains

```haskell
break :: (a -> Bool) -> [a] ([a],[a])
break _ xs@[] = (xs, xs)
break p xs@(x:xs)
	| px = ([], xs)
	| otherwise = let (ys,zs) = break p xs in (x:ys, zs)
```

1f. Comput the maximum of a non-empty list

```haskell
maximum :: Ord a => [a] -> a
maximum [] = error "Empty List"
maximum (x:xs) = max x maximum(xs)

max Ord a => a -> a -> a
max a b
	| a > b = a
	| a < b = b
	| a == b = a
```

2 We have a binary search tree built from number-string pairs, ordered by the number (acting as key)

```haskell
data Tree = Empty
	| Single Int String
	| Many Tree Int String Tree
```

and one function search partially defined over it:

```haskell
search :: Int -> Tree -> String

search x (Single i s)
	| x == i = s

search x (Many left i s right)
	| x == i = s
	| x > i = search x right
	| x < i = search x right
```

2a. Describe the two ways in which function sarch can fail, with Haskell runtime pattern-matching errors

1. Search will fail with a pattern matching error if `i` is not found within the tree 
2. Search will fail on an empty tree as there is no patter

2b. Add in error handling for function `search` above, using the `Maybe` type to ensure this function is now total. Note that this will require chaning the type of the search function.

```haskell
search :: Int -> Tree -> Maybe

search x (Empty) = Nothing

search x (Single i s)
	| x == i = Just s
	| otherwise = Nothing

search x (Many left i s right)
	| x == i = Just s
	| x > i = search x right
	| x < i = search x left
	| otherwise = nothing
```

2c. Add in generic error handling for the search function above, using monads, ensuring it is not total, and giving back a useful error message, Note that this will require changing the type (again) of the search function. 

```haskell
search :: (Monad m) => Int -> Tree -> m String

search x (Single i s)
	| x == i = return s
	| otherwise = error "Key not found"
	
search x (Empty) = error "Empty tree" 

search x (Many left i s right)
	| x == i = return s
	| x > i = search x right 
	| x < i = search x left
	| otherwise = error "Search failure"
```

