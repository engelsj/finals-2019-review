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
?- (X = 1; X = 2), !, X = Y.
X = Y, Y = 1
```

```
?- findall(X,X=Y,L).
L = [_1234]
```

```
?- setof(X, X\=1, L).
False
```

1b The predicate ``memb`` below is like ```member``` except the recursive (or inductive) clause is declared before the base case.

```
memb(X,[_|T]) :- memb(X,T).
memb(X,[X|_]).
```

How does Prolog respond to the query 

```
?- memb(X,[1,2,3]). 
```

Prolog respondes to this query as such

```
X = 3;
X = 2;
X = 1.
```

1c. Recall that the non-negative intergers can be encoded as follows

```
numeral(0).
numeral(succ(X)) :- numeral(X).
```

Define the 3-ary predicate add(X,Y,Z) and multiply(X,Y,Z) to encode addition and multiplication so that, for example,

```
?- add(succ(0), Y, succ(succ(0))).
Y= succ(0);
no.
?- multiply(succ(0), Y, succ(succ(0))).
Y= succ(succ(0));
no.
```

```
add(0,X,X).
add(succ(X), Y, succ(Z)) :- add(X,Y,Z). 

multipl(0, X, 0).
multiply(succ(X), Y, Z) :- multiply(X,Y,XY), add(XY,Y,Z).

```

1d. A binary predicate edge/2 is symmetric if whenever edge holds of a pair (a,b), it also holds (b,a). An obvious way to make edge symmetric is by adding the rule

```
edge(A,B) :- edge(B,A).
```

Why is this problematic, and how can we get around this problem whilist turning edge into a symmetric predicate symEdge?

 