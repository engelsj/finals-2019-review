s --> a(CntA), b(CntB), c(CntC), {CntB is CntA + CntC}.

a(0) --> [].
a(Count) --> [a], a(Cnt), {Count is Cnt + 1}.

b(0) --> [].
b(Count) --> [b], b(Cnt), {Count is Cnt + 1}.

c(0) --> [].
c(Count) --> [c], c(Cnt), {Count is Cnt + 1}.1a. State how a Prolog interpreter respons to the following queries, assuming no Prolog program has been consulted.

```
?- X = 1+1
X = 1+1
?- X is 1+1
X = 2
?- love(john,mary)
error
?- asset(love(john,mary))
love(john,mary)
?- .([],.(a,Y)) = [X,a]
error
?- setof(X,X=X,L).
?- findall(X,X=f(X),L).
?- X = 1, X <2.
true
?- X \= 2, X=1.
False
?- X < 2
Error --> Arguments not sufficiently instantiated
```

1b. Suppose we have the following Prolog program

```
q(a).
q(X) :- X=b,!.
q(c).
```

Write all of Prolog's answers to the following queries

```
?- q(X). --> X = a; X = b. 
?- q(X), q(Y).
?- q(X),!,q(Y).
?- q(c). --> True
```

1c. Given unary predicates bird, fly, penguin, write a Prolog program saying all birds fly except for penguins.

```
fly(X) :- bird(X) \+ penguin(X).
```

1d. Recall that positive integers can be encoded as successors of 0 and similarly, negative integers can be encoded as predecessors of 0.

```
pos(succ(0)).
pos(succ(X)) :- pos(X).

neg(pred(0)).
neg(pred(X)) :- neg(X).
```

These definitions suggest two ways to represent all integers, given by the predicates pure and mixed below.

```
pure(0).
pure(X) :- pos(X); neg(X).

mixed(0).
mixed(succ(X)) :- mixed(X).
mixed(pred(X)) :- mixed(X).
```

1di. Give a term t without variables such that Prolog answers yes/true to the following query:

```
?- mixed(t), \+ pure(t).
```

3a. What are difference lists and how are they useful?

3b. Define a DCG for the set of strings (a^n)(b^n+m)(c^m) of length 2n +2m for m >= 0. For full marks avoid the muse of extra arguments in the DCG.

```
s --> a(CntA), b(CntB), c(CntC), {CntB is CntA + CntB}.

a(0) --> [].
a(Count) --> [a], a(Cnt), {Count is Cnt + 1}.

b(0) --> [].
b(Count) --> [b], b(Cnt), {Count is Cnt + 1}.

c(0) --> [].
c(Count) --> [c], c(Cnt), {Count is Cnt + 1}.
```

3c. Write out the DCG you have in part b as ordinary Prolog clauses, making the differences lists explicit.

```
s(A,D) :- a(CntA,A,B), b(CntB,B,C), c(CntC,C,D), {CntB is CntA + CntB}.

a(0,_) :- [].
a(Count, [a|W]) :- a(Cnt, W), {Count is Cnt + 1}.

b(0,_) :- [].
b(Count, [b|W]) :- b(Cnt, W), {Count is Cnt + 1}.

c(0,_) :- [].
c(Count, [c|W]) :- c(Cnt, W), {Count is Cnt + 1}.
```

