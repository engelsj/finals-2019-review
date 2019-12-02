8.1 Here is our basic DCG:

```
s --> np(tense), vp(tense).
np(tense) --> det, n(tense).

vp(tense) --> v(tense), np(tense).
vp --> v.

det --> [the].
det --> [a].

n(singular) --> [woman].
n(plural) --> [women].

n(singular) --> [man].
n(plural) --> [men].

n(singular) --> [apple].
n(plural) --> [apples].

n(singular) --> [pears].
n(plural) --> [pear].

v(plural) --> [eats].
v(plural) --> [eat].
```

Use extra arguments to cope with the singular/plural distinction

```
s --> np(Num), vp(Num).
np(Num) --> det, n(Num).

vp(Num) --> v(Num), np(_).
vp(Num) --> v(Num).

det --> [the].
det --> [a].

n(singular) --> [woman].
n(plural) --> [women].

n(singular) --> [man].
n(plural) --> [men].

n(singular) --> [apple].
n(plural) --> [apples].

n(singular) --> [pears].
n(plural) --> [pear].

v(singular) --> [eats].
v(plural) --> [eat].
```

8.2 Translate this DCG rule into Prolog

```
kanga(V,R,Q) --> roo(V,R), jumps(Q,Q), {marsupial(V,R,Q)}.
```

```
kanga(V,R,Q,A,C) --> roo(V,R,A,B),jumps(Q,Q,B,C),marsupial(V,R,Q).
```

