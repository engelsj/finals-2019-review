##findall

```
findall(Object, Goal, List).
```

Produces a list `List` of all objects `Object` that satisfy the goal `Goal`. Oftern `Object` is simply a variable, in which case the query can be read as: *Give me a list containing all the instantiations of `Object` wich satisfy `Goal`***

## bag

```
bagof(Object, Goal, List)
```

`bag/3` is more fine grained than `final/3`. It gives us the opportunity to extract the information we want in a more structured way. Moreover, `bag/3` can also do the same job as `final/3`, with the help of a special piece of syntax, namely `^`:

```
bagof(Child,Mother^descend(Mother,Child), List)
```

This says: give me a list of all the values of Child such that `descend(Mother,Child)`, and put the result in a list, but dont worry about generating a seperate list for each value of Mother. There is one important difference between `findall/3` and `bagof/3`, namely that `bag/3` fails if the goal that is specified in its second argument is not satirized (remember, that `final/3` returns the empty list in such cases). So the query `bagof(X,descend(mary,X),Z)` yields no. 

## setof

```  
setof(Object,Goal,List)
```

The `setof/3` predicate is basically the same as `bag/3`, but with one useful difference: the lists it contains are ordered and contain no redundancies (that is, no list contains repeated items).