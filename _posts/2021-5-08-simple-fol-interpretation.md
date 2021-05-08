---
layout: post
title: A simple FOL interpretation
---

Over the last few days on Discord there have been several
discussions of the more technical sides of how Lojban can be
interpreted.  In this post, I'd like to present a
translation from a simple fragment of Lojban to first order
logic formulas.

Note that this is exclusively a syntactic translation.
There is no notion of what the formulas mean, although we
will define some axioms that will constrain the possible
interpretations.

## A minimal fragment

Lojban is a rich language, so let's start with a portion
that isn't too hard.  We will consider the following
language features:

* selbri, built up from gismu, connectives, {na}, and {be}
  constructions
* The gadri {lo}
* Existential quantification ({da}, {de}, …)
* Universal quantification ({roda}, {rode}, …)

Here is a more formal definition of the permitted
constructions.  Note that we're looking at the constructions
after parsing is complete, so terminators and words denoting
precedence do not play a role.

``
selbri -> gismu
        | {na} selbri
        | selbri {ja/je/jo} selbri
        | selbri [tag] sumti
``

``
sumti -> {lo} [tag] selbri
       | dX | rodX
``

There's a few things to note here:

* We have no notion of a bridi.  Given a bridi like {lo
  mlatu melbi} we translate this to {melbi be fa lo mlatu},
  which is a selbri in our system.
* A selbri may have a permutation applied to it to select a
  different place structure.  This is mostly a syntactic
  issue that we will not pay much attention to.
* We use tags to select which selbri places to fill, or
  which selbri place is applicable for {lo}.
* We call {da}, {de}, etc. _free variables_ in the
  remainder.


## The signature

First-order logic formulas depend on a signature, which
indicates what functions, relations, and constants are
available for use in the formula.  Note that constants are
simply nullary functions; we will thus not distinguish
between the two.

Given a selbri _s_, let _U(s)_ be the set of unfilled
places.  Note that given selbri _s_ and _t_, _U(s {ja/je/jo}
t)_ is the intersection of _U(s)_ and _U(t)_.  Let _FV(s)_
be the set of free variables of _s_.

The signature we use is as follows:

1. For every selbri _s_ with at most _n_ free variables
   (i.e. _n_ >= |_FV(s)_|) and
   every subset _A_ of _U(s)_, `Selbri[s, n, A]` is a
   relation symbol with arity _n_ + |_A_|.
2. For every sumti _a_ with at most _n_ free variables
   `Sumti[a, n]` is a function symbol with arity _n_.

With these in place, we can set out the interpretation: a
bridi is encoded as a selbri _s_, and then interpreted as a
sequence of quantifiers followed by `Selbri[s, n, {}](x, y,
...)`.  The quantifiers are interpreted in the order that
they would usually be as per the CLL.

## The theory

With the signature in place, we need to enumerate the set of
assumptions that we take as our theory, which will restrict
what interpretations are valid.

The rules are as follows.  We let _s_ and _t_ range over
selbri, and _a_ range over sumti.  _A_ (resp. _B_) is a subset of
_U(s)_ (resp. _U(t)_) and _n_ (resp. _m_) is at least
|_FV(s)_| (resp. |_FV(t)_|).  Quantifiers may range over
multiple variables.  Note that the order of variables is
supposed to be clear from context.

1. Weakening (places): Given _A'_ a subset of _A_,
   `forall x.  exists y. Selbri[s, n, A'](x, y) -> Selbri[s,
   n, A](x)`.
2. Weakening (variables): For every _n'_ >= _n_, `forall x.
   exists y. Selbri[s, n', A](x, y) <-> Selbri[s, n, A](x)`.
3. Weakening (sumti): for every _n'_ >= _n_ >= |_FV(a)_|,
   `forall x.  Sumti[a, n'](x) = Sumti[a, n](x)`.
4. Disjunction: Letting _C_ be _A_ intersect _B_ and _k_ be
   the maximum of _n_ and _m_, `forall x. Selbri[s ja t, k,
   C](x) <-> Selbri[s, k, C](x) v Selbri[t, k, C](x)`.
5. Conjunction: Letting _C_ be _A_ intersect _B_ and _k_ be
   the maximum of _n_ and _m_, `forall x. Selbri[s je t, k,
   C](x) <-> Selbri[s, k, C](x) ^ Selbri[t, k, C](x)`.
6. Implication: Letting _C_ be _A_ intersect _B_ and _k_ be
   the maximum of _n_ and _m_, `forall x. Selbri[s jo t, k,
   C](x) <-> (Selbri[s, k, C](x) -> Selbri[t, k, C](x))`.
7. Negation: `forall x. Selbri[na s, n, A](x) <-> not
   Selbri[s, n, A](x)`.
8. Application: If `tag` is not in _A_, then
   `forall x. forall y. Selbri[s tag a, n, A](x, y) <->
   Selbri[s, n, A union {tag}](x, y, Sumti[a, n](x))`.
9. Lo-Consistency: If `tag` is in _A_, `forall x. forall y.
   (exists z. Selbri[s, n, A](x, y, z)) <-> Selbri[s, n,
   A](x, y, tag: Sumti[lo tag s, n](x))`.

(This is my first guess for what the rules should be, and I
may have missed some.  Please let me know if you think some
are invalid, or if you think some rule is necessary that is
not currently present.)

## What have we got?

Let us take a look at an example.  Consider the bridi {lo
mlatu da na citka}.  The literal interpretation of this is

``
exists x. Selbri[lo mlatu da na citka, 1, {}](x)
``

However, by using the theory we can rewrite this into the
somewhat more informative

``
exists x. not Selbri[ciska (fe:da)], 1, {fa}](Sumti[lo fa mlatu, 0](), x)
``

There's still work to be done on how to best write this
down, but one can see that this is a sentence that we can
analyse more formally, asking in what models it is and isn't
true.

## Remaining work

There's a lot of it.  I was hoping to include {poi} and
{noi} in this post, but they bring in a lot of
complications.  Similarly, this post doesn't touch on the
question of number, which is absolutely essential for a
useful translation.

Going in a different direction, it would be interesting to
look further at what models there are for this theory, and
what the sumti and variables should denote.
