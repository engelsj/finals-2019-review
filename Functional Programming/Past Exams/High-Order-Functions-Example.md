2. Consider the following function definitions:

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
   f5 (x:xs) = (x * x) + f5 xs
   ```

   They all have a common pattern behaviour

   a. Write a higher-order function ```hof``` that captures this common behaviour 

   ```haskell
   -- hof [] = K
   -- hof (x:xs) = x 'op' "hof" xs
   			-- 		 = fx 'op' "hof" xs 
   hof :: r -> (b -> r -> r) -> (a -> b) -> [a] -> r
   hof k op f []  = k 
   hof k op f (x:xs) = f x 'op' hof k op f xs
   
   hof [] k op f = k
   hof (x:xs) k op f = f x 'op' hof xs k op f
   ```

   b. Rewrite each of f1 .. f2 above to be a call to hof with appropriate arguments 

   ```haskell
   f1 xs = hof 1 (*) id xs
   f2 xs = hof 0 (+) (const 1) xs 
   f3 xs = hof 0 (+) id xs
   f4 xs = hof [] (++) id xs 
   f5 xs = hof 0 (+) sqr xs  
   ```

   