

### Head - 2019, 2016 

---

Returns the first element of a list, if it is non-empty, with a runtime error otherwise. 

```haskell
head :: [a] -> a
head (x:_) = x
head [] = error "Empty List"
```

### Last - 2019

---

Returns the last element of a list, if it is non-empty, with a runtime error otherwise.

```haskell
last :: [a] -> a
last [x] = x
last (_:xs) = last xs
last [] = error "Empty List"
```

### (++) - 2019, 2018, 2014 

---

Concatenates two lists togethers 

```haskell
(++) :: [a] -> [a] -> [a]
[] ++ ys = ys
(x:xs) ++ ys = x : (xs ++ ys)
```

### Reverse - 2019, 2018, 2014 

---

Reverse its list argument

```haskell
reverse :: [a] -> [a]
reverse [] = []
reverse (x:xs) = reverse xs ++ x
```

### Span - 2019, 2016

---

Uses a predicate to split a list into two, the first being the longest prefix that satisfies the predicate, while the second lit is what remains 

```haskell
span :: (a -> Bool) -> [a] -> ([a],[a])
span p [] = ([],[])
span p (x:xs)
	| px = let (before, after) = span p xs in (x:before, after)
	| otherwise = ([], x:xs)
```

### Minimum - 2019, 2015 

---

Compute the minimum of a non-empty list 

```haskell
minimum :: Ord a => [a] -> a
minimum [] = error "Empty List"
minimum [x] = x
minimum (x:xs) = min x (minimum xs)

min :: Ord a => a -> a -> a 
min a b
	| a < b = a
	| a > b = b
	| a == b = a 
```

### Tail - 2018, 2017, 2014  

---

Returns the list with its first element removed, if it is non-empty, with a runtime error otherwise.

```haskell
tail :: [a] -> [a]
tail (_:xs) = xs
tail [] = error "Empty List"
```

### Init - 2018, 2017, 2016, 2014 

---

Returns everything but the last element of a list, if it is non-empty, with a runtime error otherwise.

```haskell
init :: [a] -> [a]
init [x] = [] 
init (x:xs) = x : init xs
init [] = error "Empty List"
```

### Break - 2018, 2014 

---

Uses a predicate to split a list into two, the first being the longest prefix that does not satisfy the predicate, while the second is what remains.

```haskell
break :: (a -> Bool) -> [a] -> ([a],[a])
break _ xs@[] = (xs, xs)
break p xs@(x:xs)
	| px = ([],xs) -- If head satifies predicate, return empty list
	| otherwise let (ys,zs) = break p xs in (x:ys, zs)
	-- Call break with the tail 
```

### Maximum - 2018, 2014  

---

Computes the maximum of a non-empty list

```haskell
maximum :: Ord a => [a] -> a
maximum [] = error "Empty List"
maximum [x] = x
maximum (x:xs) = max x (maximum xs)

max :: Ord a => a -> a -> a
max a b
	| a > b = a
	| a < b = b
	| a == b = a
```

### Last - 2017, 2016 

---

Returns the last element of a list, if it is non-empty, with a runtime error otherwise

```haskell
last :: [a] -> a
last [x] = x
last (_:xs) = last xs
last [] = error "Empty List"
```

### SplitAt - 2017, Haskell Prelude Slides

---

Split a list (its second argument) into two, the first being the prefix whose length equals the first argument (or the whole list if the list is shorter) while the second list is what remains, if anything.

```haskell
splitAt :: Int -> [a] -> ([a],[a])
splitAt n xs | n <= 9 = ([], xs)
splitAt _ [] = ([],[])
splitAt n (x:xs)
	= let (xs1, xs2) = splitAt (n - 1) xs
		in (x:xs1, xs2)
```

### Replicate- 2017, 2015

---

This function call ```replicate n x ``` returns a list that is n copies of x

```haskell
replicate :: Int -> a -> [a]
replicate 0 _ = []
replicate n x = x : replicate (n - 1) x
```

### foldl1 - 2017, 2016 

---

Take a binary function and a non-empty list of elements and use the function to reduce the list down to one value with nesting to the left. 

```haskell
foldl1 :: (a -> a -> a) -> [a] -> a 
foldl1 f (x:xs) = foldl f x xs
foldl1 _ [] = error "Empty List"

foldl :: (a -> a -> a) -> a -> [a] -> a
foldl _ z [] = z
foldl f z (x:xs) = foldl f (f z x) xs 
```

### !! - 2016

---

We can index into a list, starting from zero. So ```xs !! n ``` returns (n + 1)th element of ```xs``` provided n is non-negative and the length of the list is long enough. Otherwise, we get a run-time error

```haskell
!! :: [a] -> Int -> a
xs !! n | n < 0 = error "Negative Index"
[] !! _ = error "Index too Large"
(x:_) !! 0 = x
(_:xs) !! n = xs !! (n - 1)
```

### Null - Haskell Prelude Slides

---

Returns true if the list is empty

```haskell
null :: [a] -> Bool
null [] = True
null (_:_) = False
```

### Take - Haskell Prelude Slides

---

Returns a specified number of elements from a specified list

```haskell
take :: Int -> [a] -> [a]
take n _ | n <= 0 = []
take _ [] = []
take n (x:xs) = x : take (n - 1) xs
```

### Drop - Haskell Prelude Slides

---

Drops a specific number of elements from the beginning of a list. 

```Haskell 
drop :: Int -> [a] -> [a]
drop n xs | n <= 0 = xs
drop _ [] = []
drop n (x:xs) = drop (n - 1) xs
```

### Concat - 2015

---

Concat joins a list of lists together into a single list

```haskell
concat :: [[a]] -> [a]
concat = foldr (++) []

foldr :: (a -> b -> b) -> b -> [a] -> b
foldr _ z [] = z
foldr f z (x:xs) = f x (foldr f z xs)
```

### Zip - 2015

---

Creates a new list by joining elements at the same index in two input lists into pairs

```haskell
zip :: [a] -> [b] -> [(a,b)]
zip _ [] = []
zip [] _ = []
zip (x:xs) (y:ys) = (x,y):zip xs ys
```

### Unzip - 2015

---

Converts a list of pairs into a pair of lists by sending the first element of each input pair to one list and the second element to another 

```haskell
unzip :: [(a,b)] -> ([a], [b])
unzip [] = ([],[])
unzip((a,b):xs) = (a : i, b: i)
	where i = unzip xs 
```

