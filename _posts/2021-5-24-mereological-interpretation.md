---
layout: post
title: A mereological interpretation
---

Thanks to Ntsékees, I got around to reading [a little about
mereology today][2] [[1]] and I found it remarkably fitting for an
interpretation of Lojban, especially in the context of the
recent {lo} vs {loi} discussions on [roljbogu'e][0].  So
without further ado, let's see what we can cobble together!

Disclaimer: this is totally untested.  I think it's a
promising direction and would love some feedback on it, but
it's nowhere close to a complete solution.

## Mereology

In mereology, we look at a system by considering the
parthood relation.  Consider a group of people moving a
piano.  In set theory, we may model this as a set of people;
the components of the individual people, are not themselves
elements of this set.  This can be seen as a _structured
parthood_ relation, where only the components that are
structurally constituting the whole are seen as being parts
in the relevant sense.
In mereology, all the parts of the
people are seen as parts of the group; we thus focus on
_unstructured parthood_.

The system I present here is a small variation of the system
of classical extensional mereology (CEM) described in [[1]].

Let $$(P, \le)$$ be a poset.  Given $$x, y \in P$$, we say
that $$x$$ and $$y$$ overlap, denoted $$x \circ y$$ if there
exists a $$z$$ such that $$z \le x$$ and $$z \le y$$.  Given
a subset $$X$$ of $$P$$, we say that $$x$$ is the _sum_ of
$$X$$ if

$$
\forall y. (y \circ x \leftrightarrow \exists z \in X. y \circ z).
$$

We say that $$(P, \le)$$ is a mereological space with
respect to some class of sets $$\mathcal{X}$$ if for every
non-empty subset $$X \in \mathcal{X}$$, the sum exists and
is unique.  We denote the sum of $$X$$ by $$\oplus X$$ and
of $$\{x, y\}$$ by $$x \oplus y$$.


## Conceptual entities

When speaking, we have "conceptual" entities in mind: this
cup, this tea, this friend.  For the purposes of this
interpretation, we assume that such a set of entities $$P$$ is
fixed ahead of time.  We assume the existence of an
unstructured parthood relationship $$\le$$ on $$P$$, which
makes $$(P, \le)$$ into a mereological space with respect to
conceptualisable sets.

Our interpretation of structured parthood for an element
$$x \in P$$ will be given by taking another conceptualisable
set of elements $$X$$ of $$P$$ such that $$\oplus X \le x$$.
Let $$S$$ be the set of such pairs; we will interpret sumti
as elements of $$S$$.

## Interpreting {lo} and {loi}

Let us start by looking at the interpretation of {PA lo PA
broda} and {PA lo PA loi PA broda} for cases when none of
the {PA} are {no}.  We use SOL for the formalisation, where
capital letters range over conceptualisable subsets of $$S$$
and lowercase letters range over elements of $$S$$.

Let us introduce a little terminology to distinguish the
quantifiers.  In {pa lo re broda}, we call {pa} the _local_
quantifier and {re} the _global_ quantifier.  In {pa lo re
loi ci broda}, we do the same, and call {ci} the _grouping_
quantifier.  We will use $$i$$ for the global quantifier,
$$j$$ for the local quantifier, and $$k$$ for the grouping
quantifier.

We assume that all selbri variables are interpreted as
relations on $$S$$, with {brodA} interpreted by $$R_A$$.

The translation proceeds as follows.  For every {brodA} with
its global quantifier $$i$$, introduce a second-order
constant $$B_A$$.  The default global quantifier for {lo} is
{ro}, while the default global quantifier for {loi} is
{su'o}.  Add the following to the theory:

1. If the gadri is {lo}, $$\forall (x, X) \in B_A. R_A(x)$$.
2. If the gadri is {loi}, $$\forall (x, X) \in B_A.
   \forall y \in X. R_A(y)$$ and $$\forall (x, X) \in B_A. x = \oplus X$$.
3. If $$i$$ is a cardinality constraint, the requirement
   that $$|B_A|$$ satisfies $$i$$.
4. If the gadri is {lo} and $$i$$ is {ro}, $$\forall x. R_A(x) \to x \in
   B_A$$.
5. If the gadri is {loi} and $$i$$ is {ro}, $$\forall
   x. R_A(x) \to \exists (y, Y) \in B_A. x \in Y$$.
6. If there is a grouping quantifier $$k$$, add the
   requirement $$\forall (x, X) \in B_A. |X| = k$$ if $$k$$
   is a cardinal, and $$\forall (x, X) \in B_A. \forall y.
   R_A(y) \to y \in X$$ if $$k$$ is {ro}.

For every {brodA} with inner quantifier $$j$$, add a
quantifier $$Q_j s_A \in B_A$$ to the resulting
formula.  Within all these quantifiers, instantiate the
selbri with the variables $$s_A$$ for every $$A$$.  If any
variables has a grouping quantifier $$k$$, also add the
requirement that if $$s_A = (x, X)$$, then the cardinality
of $$X$$ is $$k$$.  (If $$k$$ is {ro}, require that for every
$$y$$ such that $$R_A(y)$$, $$y \in X$$.)

## Let's look at an example!

Let's translate the sentence {lo re broda ku ci lo vo loi
mu brode ku brodi}.  Right away, we see we'll need two
constants $$B_A$$ and $$B_E$$.  The theory
consists of the following statements:

* $$\forall (x, X) \in B_A. R_A(x)$$.
* $$\vert B_A \vert = 2$$.
* $$\forall (x, X) \in B_E. \forall y \in X. R_E(y)$$.
* $$\forall (x, X) \in B_E. x = \oplus X$$.
* $$\vert B_E \vert = 4$$.
* $$\forall (x, X) \in B_E. \vert X \vert  = 5$$.

The formula itself is

$$
\forall s_A \in B_A. \exists^{=3} s_E \in B_E. R_I(s_A,
s_B).
$$

This doesn't look too bad.  Let's say {broda} is "$$x_1$$ is
a question", {brode} is "$$x_1$$ is a person", and {brodi}
is "$$x_1$$ is solved by $$x_2$$".  Then we get a set of two
questions and a set of four groups of five people each,
where exactly three groups of people solved each question.
This seems to be a reasonable interpretation!

## {lo bevri}

This discussion was largely motivated by la ziren's question
of whether, after one says {loi prenu cu bevri}, one can say
{lo bevri} to refer to the mass of people.  As is clear from
the above, my answer is: yes!  There is no semantic
difference between masses and non-masses, massing is simply
a useful way to get the structural parthood relationship
right.  Note that for {lo}, we allow any structural
parthood relationship.  {lo bevri} recovers the value of the
$$x_1$$ of {bevri}, which is the same $$(x, X)$$ pair as we
got from {loi prenu}.

## Further work

First of all: once again, this is a back-of-the-napkin
attempt that should not be taken all too seriously.  I think
that first of all, a lot more effort needs to go into
checking how this works out for common sentences and making
sure there are no unreasonable consequences.

However, that said, I do think there's something promising
to this approach.  It seems to me like the connective {jo'u}
could be interpreted as mapping $$(x, X)$$ and $$(y, Y)$$ to
$$(x \oplus y, X \cup Y)$$, contrasting it with {ce}, which
would map them to $$(x \oplus y, \{x, y\})$$.

An interesting question is how this interpretation could
influence the way selbri are defined: definitions that are
aware of this structure could perhaps be more specific than
the current ones.

One thing I'd like to do is see what kind of interesting
things can be said if we take $$P$$ to contain the natural
numbers and the computable sets of natural numbers.  (It's
not entirely clear how the empty set fits into this,
though!)

Another thing that I'd like to try, since I don't think it
worked out all that well here, is to try to model the
distributivity of global quantifiers as part of the objects
themselves, rather than as something additional on top of
them.

Thanks for reading, and huge thanks to la ziren, Ntsékees,
and la .dram. for discussions on this topic!  Once again,
all feedback is very welcome, be it on [roljbogu'e][0] or
[Twitter](https://twitter.com/jesyspa)!

## References

1. Lucas Champollion, Manfred Krifka, _Mereology_, Cambridge
   Handbook of Formal Semantics. ([lingbuzz/002099][2])
{: #ChampollionKrifka}


[0]: https://discord.com/invite/dGP5A6Fpj7
[1]: #ChampollionKrifka
[2]: https://ling.auf.net/lingbuzz/002099
