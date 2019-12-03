9.1 Which of following queries succeed, and which fail?

```
12 is 2*6 --> Succeed
14 =/= 2*6 --> succeed
12 = 2*7 --> Failes
14 == 2*7 --> Failes
14 \== 2*7 --> Succeed
14 =:= 2*7 --> Succeed
[1,2,3|[d,e]] == [1,2,3,d,e] --> Succeed
2+3 == 3+2 --> Fails
2+3 =:= 3+2 --> Succeed
7-2 =\= 9-2 --> Succeed
p == 'p' --> succeed
p =\= 'p' --> error
vincent == VAR. --> fails
vincent = Var, VAR == vincent --> succeed
```

9.2 How does Prolog respond to the following queries?

```
.(a,.(b,.(c,[]))) = [a,b,c]. --> True
.(a,.(b,.(c,[]))) = [a,b,|[c]] --> True
.(.(a,[]),.(.(b,[]),.(.(c,[]),[])) = X
X = [[a],[b],[c]]
.(a,.(b,.(.(c,[]),[]))) = [a,b|[c]] --> False
```

9.3 Write a two-place predicate `termtype(Term,Type)` that takes a term and gives back the type(s) of that term (atom, number,constant,variable, and so on). The types should be given back in the order of their generality. 

```
termtype(Term, atom) :- atom(Term).
termtype(Term, number) :- number(Term).
termtype(Term, constant) :- atomic(Term).
termtype(Term, variable) :- var(Term).
termtype(Term,simple_term) :- var(Term).
termtype(Term, complex_term) :- nonvar(Term), functor(Term,_,Arity), Arity > 0
termtype(Term, term) :- termtype(Term, simple_term)
termtype(Term,term) :- termtype(Term, complex_term)
```

9.4 Write a Prolog program that defines the predicate groundTerm(Term) which tests whether or not Term is a ground term. Ground terms are terms that don't contain variables. 

```
groundterm(Term) :- atomic(Term).
groundterm(Term) :- nonvar(Term), functor(Term,_,Arity), groundTerm(Term,Arity).
groundterm(_,0).
groundterm(ComplexTerm,arg) :- Arg > 0. arg(Arg, ComplexTerm,Term), groundterm(Term), Nexter Arg is Arg - 1, groundterm(ComplexTerm, NextArg)
```

.