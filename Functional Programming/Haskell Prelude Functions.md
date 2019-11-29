## Haskell Prelude Functions

### head

---

```head xs ``` returns the first element of ```xs``` , if the list is non-empty

```haskell
head :: [a] -> a -- Type signature 
head (x:_) = x -- Non-Empty List
head [] = error "Prelude.head: empty list" -- Empty List
```

###tail

---

``` tail xs ```, for non-empty ```xs``` returns it with first element removed

```haskell
tail :: [a] -> [a] -- Type Signature
tail (_:xs) = xs -- Non-Empty List
tail [] = error "Prelude.tail: empty list" -- Empty List
```

### last

---

```last xs ``` returns the last element of ```xs```, if non-empty

```Haskell
last :: [a] -> a -- Type Signature
last [x] = x -- Singleton list, most occur before (_:xs)
last (_:xs) = last xs -- Non-Empty List
last [] = error "Prelude.last: empty list" -- Empty List
```

### init 

---

``` init xs```, for non-empty ```xs``` reutrns it with last element removed

```Haskell
init :: [a] -> [a] -- Type Signature
init [x] = [] -- Singleton List
init (x:xs) = x : init xs -- Non-Empty List 
init [] = error "Prelude.init: empty list" -- Empty List 
```

### null

---

```null xs``` returns ```True``` if the list is empty 

```Haskell
null :: [a] -> Bool -- Type Signature
null [] = True -- Empty List
null (_:_) = False -- Non-Empty List
```

### ++ 

---

``` xs ++ ys``` joins lists ```xs``` and ```ys``` together 

```haskell
(++) :: [a] -> [a] - [a] -- Type Signature
[] ++ ys = ys -- Empty List
(x:xs) ++ ys = x : (xs ++ ys) -- Non-Empty List
```

### reverse (Slow with ++ function)

---

``` reverse xs ``` reverses the list ``` xs``` 

```haskell
reverse :: [a] -> [a] -- Type Signature 
reverse [] = [] -- Empty List
reverse (x:xs) = reverse xs ++ [x]  -- Non-Empty List

(++) :: [a] -> [a] - [a] -- Type Signature
[] ++ ys = ys -- Empty List
(x:xs) ++ ys = x : (xs ++ ys) -- Non-Empty List
```

### (!!)

---

``` (!!) xs n```,or ``` xs !! n ``` selects the ```n```th element of list ```xs``` , provided it is long enough. Indices start at 0.

```haskell
(!!) :: [a] -> Int -> a -- Type Signature
xs !! n | n < 0 = error "Prelude.!!: negative index" -- Negative Index
[] !! _ = error "Prelude.!!: index too large" -- Empty List
(x:_) !! 0 = x -- Zero Index
(_:xs) !! n = xs !! (n - 1) -- Non-Zero Index
```

### take

---

Returns a specified number of elements from a specified list. For instance ``` take 3 [5,4,3,2,1] ``` will return ```[5,4,3]```. 

```Haskell
take :: Int -> [a] -> [a] -- Type Signature 
take n _ | n <= 0 = [] -- If n is <=0 just return []
take _ [] = [] -- If the [] then return []
take n (x:xs) = x : take (n - 1) xs -- 
```

### drop 

----

Drops the specified number of elements from the beginning of a list

```Haskell
drop :: Int -> [a] -> [a]
drop n xs | n <= 0 = xs
drop _ [] = []
drop n (n:xs) = drop (n - 1) xs
```

### splitAt 

---

Splits a given into two lists at a specified index 

```haskell
splitAt :: Int -> [a] -> ([a], [a])
splitAt n xs | n <= 0 = ([], xs)
splitAt _ [] = ([],[])
splitAt n (x:xs) 
	= let (xs1, xs2) = splitAt (n - 1) xs
	in (x:xs1, xs2)
```

### span

---

Uses a predicate to split a list into two, the first list being the longest prefix that satisfies the predicate, while the second list is what remains.



### minimum

---

Finds the smallest value in a non-empty list. The class constraint (Ord a) ensures that the operation of the typecalss ```Ord``` work on items in the list. 

```haskell
minimum :: Ord => [a] -> [a]
minimum [] = error "Maximum of empty list"
minimum [x] = x
minimum (x:xs) = min x (maximum xs)
```

### maximum 

---

Takes a list of orderable things and returns the largest of them

```haskell
maximum :: (Ord a) => [a] -> a
maximum [] = error "Maximum of empty list"
maximum [x] = x
maximum (x:xs) = max x (maximum xs)
```

### replicate 

---

Takes an ```Int``` and a value and returns a list that has several repititions of that value 

```haskell
replicate :: Int -> a -> [a]
replicate n x
	| n <= 0 = []
	| otherwise = x : replicate (n - 1) x 
```

### break

---

Uses a predicate to split a list into two, the first being the longest prefix that does not satisfy the predicate, while the second list is what remains

```haskell
break :: (a -> Bool) -> [a] -> ([a],[a])
```

### repeat 

---

The ```repeat``` function takes an element and returns and infinite list composed of that element. 

```haskell
repeat :: a -> [a]
repear x = x : repeat x
```

### concat

---

Joins a list of lists together into a single list. For example ```concat [[1,2], [3]]``` creates the list ```[1,2,3]``` 

### zip

---

The ``` zip ``` function takes two lists and zips them together. For instance, calling ```zip [1,2,3] [7,8]``` returns ```[(1,7),(2,8)]``` 

```haskell
zip :: [a] -> [b] -> [(a,b)]
zip _ [] = []

```



### unzip 

---

converts a list of pairs into a pair of lists by sending the first element of each input pair to one list, and the second element to another. For example, ```unzip [(1, 4), (2, 5),(3,6)]``` creates the pair ```([1,2,3], [4,5,6])```. Unzipping the empty list results in a pair of empty lists 

### dropWhile

---

### filter 

---



### foldr1 

---



### foldl1 

---

Take a binary function and a non-empty list of elements and use the function to reduce the list down to one value with nesting to the left.

```haskell
foldl1 :: (a -> a -> a) -> [a] -> a 
```

