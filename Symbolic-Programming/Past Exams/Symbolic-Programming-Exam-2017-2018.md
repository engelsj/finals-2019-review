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
L = [_1234]

?- findall(X,X=f(X),L).
L = [_1234],
	_1234 = f(_123)

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

Difference lists represent the information about grammatical categories not as a single list, but as the difference between two lists. Through the use of difference lists, programmers can avoid inefficient, repetitive calls to `append/3`. This is because the program looks to consume each part of the list and  then check if the resulting list is empty, meaning that every piece of grammar within the list has been properly consumed.

3b. Define a DCG for the set of strings (a^n)(b^n+m)(c^m) of length 2n +2m for m >= 0. For full marks avoid the muse of extra arguments in the DCG.

```
s --> a, b.
a --> [].
a --> [a], a, [b].
b --> [].
b --> [b], b, [c].
```

3c. Write out the DCG you have in part b as ordinary Prolog clauses, making the differences lists explicit.

```
s(A,D) :- a(A,C), b(C,D).

a([],W).
aa([a|W], W).
ab([b|W], W).
a(A,D):- aa(A,B), a(B,C), ab(C,D).

b([],W).
b(A,D):- bb(A,B), b(B,C), bc(C,D).
bb([b|W], W).
bc([b|W],W).
```

