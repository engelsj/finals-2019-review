10.1 Suppose we have the following database:

```
p(1).
p(2) :- !.
p(3).
```

Write all of Prolog's answers to the following queries:

```
?- p(X).
X = 1;
X = 2.

?- p(X), p(Y).
X = 1, Y = 1;
X = 1, Y = 2;
X = 2, Y = 1;
X = 2, Y = 2.

?- p(X),!, p(Y).
X = 1, Y = 1;
X = 1, Y = 2.
```

10.2 First, explain what the following program does:

```
class(Number,positive) :- Number > 0.
class(0, zero).
class(Number, negative) : Number < 0. 
```

This program classifies if a number is positive, negative, or zero. 

Second, improve it by adding green cuts

```
class(Number, positive) :- Number > 0, ! .
class(0, zero) :- !.
class(Number, negative) :- Number < 0, !.
```

10.3 Without using cut, write a predicate split/3 that splits a list of integers into two lists: one containing the positive ones (and zero), the other contains the negative ones.

```
split([],[],[]).
split([Number|L], Pos, [Number|Neg]) :- Number < 0, split(L, Pos, Neg). 
split([Number|L],[Number|Pos], Neg) :- Number >= 0, split(L, Pos, Neg). 
```