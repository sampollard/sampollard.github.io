+++
title = "Ltac Adventures"
date = 2020-06-10
description = "Ltac is a strange, dynamically typed language..."
+++

Ltac is a strange, dynamically typed language used to write tactics in Coq.
In some sense it's the polar opposite of Coq because of how little is
typechecked.  Upon first blush, Ltac looks sort of like Gallina, but the
semantics are very different. Here I'm just putting notes together for tips and
tricks to manage learning it. If you're like me, then the [Ltac reference
manual](https://coq.inria.fr/refman/proof-engine/ltac.html) causes more
confusions than it clears up, so I'll be trying to post in more plain English.

I'll start with my motivation for developing some proof automation, then go through
my thought process. Feedback is greatly appreciated but I wanted to present a more
informal approach since the Ltac manual is not friendly to newcomers.

#### Spotting Errors

Your most valuable friend when debugging Ltac is `idtac`, which is the tactic
that both does nothing and sends a message to the console.

In my case, I am working with floating point numbers both as bits and as
abstract data types, specifically, those used in Flocq. For these, I need to
prove a whole slew of rather uninteresting lemmas about numbers. In Coq, these
may take the form of relations of `Z`, `nat`, `N`, `positive`s, and since I'm
dealing with bits needs bounds on the number of bits needed to represent a
number; that way we know no overflow occurs, to name one case.

For example, suppose you have the following

```
Ltac add_hyp_before_lia A :=
  try match goal with
    | [ p1 : positive, p2 : positive |- _ ] =>
        pose proof (A p1)
      ; pose proof (A p2)
  end;
  lia.
```

Do you spot the mistake? There is no semicolon `;` between the two `pose
proof`s. This means the match tactic will always fail. But since we wrapped
the whole match inside a `try`. But there will not be any indication that
this tactic inside of `try` will *never* work.

I figured this out by adding the following line:

```
Ltac add_hyp_before_lia A :=
  try match goal with
    | [ p1 : positive, p2 : positive |- _ ] =>
	  idtac "trying to add 2 hypotheses"
      pose proof (A p1)
      pose proof (A p2)
  end;
  lia.
```

