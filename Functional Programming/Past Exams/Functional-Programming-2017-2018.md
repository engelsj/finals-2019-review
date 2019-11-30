## Section A

a. Returns the list with its first element removed, if it is non-empty, with a runtime error otherwise.

```haskell
tail :: [a] -> [a]
tail (_:xs) = xs
tail [] = error "Empty List"
```

b. Concatenate two lists together 

```haskell
(++) :: [a] -> [a] -> [a]
[] ++ ys = ys
(x:xs) ++ ys = x :(xs ++ ys)
```

c. Returns everything but the last element of a list, if it is non-empty, with a runtime error otherwise.

```Haskell
init :: [a] -> [a]
init [x] = []
init (x:xs) = x : init xs
init [] = error "Empty List"
```

d. Reverse its list argument

```haskell
reverse :: [a] -> [a]
reverse [] = [] 
reverse (x:xs) = reverse xs ++ [x]

(++) :: [a] -> [a] -> [a]
[] ++ ys = ys
(x:xs) ++ ys = x :(xs ++ ys)
```

e. Use a predicate to split a list into two, the first list being the longest prefix that does not satisfy the predicate, while the second list is what remains

```haskell
break :: (a -> Bool) -> [a] ([a],[a])
break _ xs@[] = (xs, xs)
break p xs@(x:xs)
	| px = ([], xs)
	| otherwise = let (ys,zs) = break p xs in (x:ys, zs)
```

f. Comput the maximum of a non-empty list

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

