## Section A

a. Returns the list with its first element removed, if it is non-empty, with a runtime error otherwise.

```haskell
tail :: [a] -> [a]
tail [] = error "Empty List"
tail [x] = [] 
tail (x:xs) = x
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
init [] = error "Empty List"

```
