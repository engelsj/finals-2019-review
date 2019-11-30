1a State how a Prolog interpreter responds to the following queries, assuming no Prolog program has been consulted.

```
? - [1,2] = [X|Y]
X = 1,
Y = [2].
```

```
?- X is 0 + Y.
Argument are not sufficiently instantiated 
```

```
?- X = 0 + Y.
X = 0 + Y
```

```
?- <(0,1).
True
```

```
% Think this should work?
?- assert(r(a)), r(a).
Undefined procedure r/1
```

```
?- retract(r(a)), r(a), assert(r(a)).
Undefined procedure r/1
```

```
? (X=1;X=2), Y = X+1
X = 1,
Y = 1 + 1;
X = 2,
Y = 2 + 1;
```

```

```

