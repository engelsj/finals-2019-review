## 2017 

Consider the following function definitions:

```haskell
f1 [] = 42
f1 (x:xs) = x * f1 xs

f2 [] = 0
f2 (x:xs) = 99 * f2 xs

f3 [] = 0
f3 (x:xs) = x + f3 xs

f4 [] = []
f4 (x:xs) = x ++ f4 xs

f5 [] = 0
f5 (x:xs) = (x - 42) + f5 xs
```

2a Write a higher-order function `hof` that captures this common behaviour 

```
hof :: a -> (a -> a -> a) -> (a -> b) -> [a] -> r 
hof k op f [] = k
hof k op f (x:xs) = f x 'op' hof k op f xs
```

2b. Rewrite each 

```
f1 xs = hof 42 (*) (id) xs
f2 xs = hof 0 (*) (const 1) xs
f3 xs = hof 0 (+) (id) xs
f4 xs = hof [] (++) (id) xs
f5 xs = hof 0 (+) (subtract 42) xs
```

## 2016

Consider the following function definitions:

```
f1 [] = 1
f1 (x:xs) = x * f1 xs

f2 [] = 0
f2 (x:xs) = 1 + f2 xs

f3 [] = 0
f3 (x:xs) = x + f3 xs

f4 [] = []
f4 (x:xs) = x ++ f4 xs

f5 [] = 0
f5 (x:xs) = (x*x) + f5 xs
```

2a. Write a higher-order function `hof` that caputes this common behaviour 

```
hof :: a -> (a -> a -> a) -> (a -> a) -> [a] -> a
hof k op f [] = k
hof k op f (x:xs) = f x 'op' hof k op f xs 
```

2b. Rewrite each of `f1`, `f2` ... above to be a call to `hof` with appropriate arguments

```
f1 xs = 1 (*) (id) xs
f2 xs = 0 (+) (const 1) xs
f3 xs = 0 (+) (id) xs
f4 xs = [] (++) (id) xs
f5 xs = 0 (+) (sqr) xs
```

