# clj-prolog

A simple implementation of a subset of prolog, a logic programming
language, in Clojure.

This is heavily based on the prolog in lisp implementation by Peter
Norvig in
[Paradigms of AI Programming: Case Studies in Common Lisp](http://www.amazon.com/gp/product/1558601910/ref=as_li_ss_tl?ie=UTF8&tag=pseudofish-20&linkCode=as2&camp=217145&creative=399369&creativeASIN=1558601910)

If you actually want to write logic programs in Clojure, please use
the logic programming features for Clojure in
[core.logic](https://github.com/clojure/core.logic)

Note: This is still very much under development, as I am using this as
a way of learning clojure by writing more code.

## Usage

Creation of rules & facts:

``` clojure
(<- (likes Kim Robin))
(<- (likes Sandy Lee))
(<- (likes Sandy Kim))
(<- (likes Robin cats))
(<- (likes Sandy ?x) (likes ?x cats))
(<- (likes Kim ?x) (likes ?x Lee) (likes ?x Kim))
(<- (likes ?x ?x))
```

Basic interaction:

``` clojure
user> (use :reload 'clj-prolog.core)
nil

user> (?- (likes Sandy ?who))

?who = Sandy;
?who = cats;
?who = Sandy;
?who = Robin;
?who = Kim;
?who = Lee;
nil

user> (?- (likes ?who Sandy))

?who = Sandy;
?who = Kim;
?who = Sandy;
nil

user> (?- (likes Robin Lee))
No.
nil
```

Unification:

``` clojure
user> (use :reload 'clj-prolog.unify)
nil 
user> (unify '(?x + 1) '(2 + ?y))
((?y 1) (?x 2))
```

## License

Copyright (C) 2011 Geoff Wilson

Distributed under the Eclipse Public License, the same as Clojure.
