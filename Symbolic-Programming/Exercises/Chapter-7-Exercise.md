7.1 Suppose we are working with the following DCG:

```
s --> foo,bar,wiggle. 
foo --> [choo].
foo --> foo,foo.
bar --> mar,zar.
mar --> me,my.
me --> [i].
my --> [am].
zar --> blar,car.
blar --> [a].
car --> [train].
wiggle --> [toot].
wiggle --> wiggle, wiggle. 
```

Write down the ordinary prolog rules that correspond to these DCG rules. What are the first three responses to the query s(X,[])?

```
s(A,B) :- foo(A,C), bar(C,D), wiggle(D,B).
foo([choo|W],W).
foo(A,B) :- foo(A,C), foo(C,B).
bar(A,B) :- mar(A,C), zar(C,B).
mar(A,B) :- me(A,C), my(C,B).
me([i|W],W).
my([am|W],W).
zar(A,B) :- blar(A,C), car(C,B).
blar([a|W],W).
car([train|W],W).
wiggle([toot|W],W).
wiggle(A,B) :- wiggle(A,C), wiggle(C,B).
```

7.2 The formal language a^n b^n consists of all the strings in a^n b^n except the empty string. Write the DCG that generates this language.

```
s --> [a,b].
s --> a, s, b.
a --> [a].
b --> [b].
```

7.3 Let a^n b^2n be the formal language which contains all strings of the following form: an unbroken block of as of length n followed by an unbroken block of bs of length 2n and nothing else. Write a DCG that generates this langauge.

```
s --> [].
s --> a, s, b.
a --> [a].
b --> [bb]. 
```

