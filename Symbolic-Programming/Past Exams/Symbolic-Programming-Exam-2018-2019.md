--1a State how a Prolog interpreter responds to the following queries, assuming no Prolog program has been consulted.

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

```
symEdge(A,B) :- edge(A,B); edge(B,A). 
```



3a. What are difference list and how are they useful?



3b. A simple DCG for generating bit strings (i.e. lists of 0 and 1) is

```
s --> [].
s --> s,b.

b --> [0].
b --> [1].

% For Example
?- s(L,[]).
L = [] ? ;
L = [0] ? ;
L = [1] ? ;
L = [0,0] ? ;
L = [0,1] ? ; 
L = [1,0] ? ;
L = [1,1] ? ;
L = [0,0,0] ? ;
```

But what is problematic about the query 

```
? - s([a],[])
```

and how can we fix the DCG above so that the Prolog interpreter answers no to this query.

Having s 

3c. Write out the DCF given in part (b) as ordinary Prolog clauses, making the difference lists explicit

```
s(A,A).
s(A,B) :- s(A,C), b(C,B).
b([0|B],B).
b([1|B],B).
```

3d. 

Write a DCG for a predicate s that outputs lists of the form

[b1,b2, ..., bnk]

for every integer n >= 0 such that bi is either 0 or 1 for 1 <= i <=n and k is the integer that the bitstring b1b2 ... bn encodes. 

```
s --> b(_Length, N), [N].
b(1,0) --> [0].
b(1,1) --> [1].
b(L,N) --> [0], b(L1,N1) {L is L + 1, N is N1}
b(L,N) --> [1], b(L1,N1) {L is L + 1, N is N1 + 2 ^ L1}
```

3e. Write a DCG that outputs strings of the form

```
[Stu1, Spo1, Cou1, Stu2, Spo1, Cou2, Stu3,Spo3,Cou3]
```

```
s --> 	student(Stu1), sport(Spo1), county(Cou1), 
		student(Stu2), sport(Spo2), county(Cou2), 
		student(Stu3), sport(Spo3), county(Cou3), 

		{Stu1 \= Stu2, Stu1 \= Stu3, Stu2 \= Stu3},
		{Cou1 \= Cou2, Cou1 \= Cou3, Cou2 \= Cou3},
		{Spo1 \= Spo2, Spo1 \= Spo3, Spo2 \= Spo3}.

student('chris') --> [chris].
student('pat') --> [pat].
student('sandy') --> [sandy].

sport('boxing') -->[boxing].
sport('football') -->[football].
sport('tennis') -->[tennis].

county('cork') --> [cork].
county('dublin') --> [dublin].
county('mayo') -->[mayo]. 
```



 