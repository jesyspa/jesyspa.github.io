---
layout: post
title: Joining bridi
---

I'm currently learning Lojban and one topic that has given
me some trouble is the variety of ways in which bridi can be
put together.
By writing this post I'd like to gather all my understanding
of the grammar for this in one place.

See my post on [my bankle][0] for details on how my language
deviates from CLL Lojban.
If any of this deviates more than described there, please
let me know!

Throughout the post I'll use _X_ and _Y_ to denote arbitrary
bridi.  There are three kinds of relations between bridi
that I'll look at:

1. Binary connectives, both logical and non-logical:
   {je}, {joi}...
2. Tenses:  {ca}, {co'a}, {pu zi zu'a}...
3. Modals:  {ki'u}, {va'o}...

**Acknowledgements:** I'd like to thank the community of
the [roljbogu'e Discord server][3], in particular la srasu,
for explaining all this to me.  All mistakes are mine.

## Modality

The simplest way to connect two bridi with a tense or a
modal is to wrap one of them into an abstraction and then
put them together.  If you'd like to say that _X_ happens
with justification _Y_, for example, you can say

> _X_ ki'u lo nu _Y_

The same can be done with tenses, for example to say that
_X_ happens after _Y_:

> _X_ ba lo nu _Y_

The event of _Y_ is the reference point, from which you go
into the future, and end up at _X_.

## Sentence links

If your bridi are sentences in their own right, then they
can be joined by putting one after the other with {.i}
inbetween.
This does not imply any explicit relation between the two.
The [new sentence links][2] allow for more connections,
which hint at a relation but do not specify it explicitly.

### Relating the bridi

A relation can be inserted explicitly by placing it after
the sentence link.  A conjunction, for example, goes as
follows:

> _X_ .i je _Y_

For modals and tenses, {bo} must be added.

> _X_ .i ba bo _Y_
>
> _X_ .i ki'u bo _Y_

Tenses and modals behave differently in this context.  In
the case of a modal, this is similar to using the modal
directly as in the section above
For a tense, however, the direction flips, so the above is
closer to

> _Y_ ba lo nu _X_

The intuition is that you have claimed _X_, and are now
making your imaginary journey onwards to _Y_.

### A difference with modality

Another subtle difference here is that since both bridi are
sentences by themselves, strictly speaking they are both
being claimed.  For example,

> mi gleki va'o lo nu mi citka

expresses "When I eat, I am happy", while

> mi gleki .i va'o bo mi citka

is hard to translate to English but _probably_ states that I
am happy.  (A reading I could also see being valid is "I am
happy.  When I'm eating, anyway.")

The distinction is more clear with tenses, where

> mi gleki .i pu bo mi citka

is unambiguously "I am happy.  Before that, I ate." and
says something very different than

> mi citka pu lo nu mi gleki

which translates to something closer to "I ate before I was
happy."

## Forethought connection

A more explicit connection is through forethought
connectives.  These are just like using modality, except you
put the connective first.  An advantage here is that the
bridi does not need to be wrapped in an abstraction;
however, it is also not quite clear to me whether it is
being claimed.

### New style: {ga je _X_ gi _Y_}

In the [simplified connective system][1], forethought
connectives can all be made using the given form, and
resemble the way sentence link connectives work:

> ga je _X_ gi _Y_
>
> ga ki'u bo _X_ gi _Y_
>
> ga pu bo _X_ gi _Y_

As far as I can tell, the anchoring point for the {bu} is
_X_, not _Y_, so in this case _Y_ is said to happen before
_X_ does.

### Old style: {je gi _X_ gi _Y_}

Another way of writing forethought connectives is by putting
the connective before a {gi}.  In the CLL, this is highly
restricted—you can only do it with JOI.  However, it's
great for modals and tenses since you don't need the {bo}:

> ki'u gi _X_ gi _Y_
>
> pu gi _X_ gi _Y_

**Note:** Thanks to la ziren for clarifying this bit!

## Summary

So to put it all together, all the following can occur, with
the following rough translations:

* {_X_ ki'u lo nu _Y_} — "_X_ because _Y_"
* {_X_ pu lo nu _Y_} — "_X_ before _Y_"
* {_X_ .i je _Y_}  — "_X_ and _Y_"
* {_X_ .i pu bo _Y_} — "_X_, before that _Y_"
* {_X_ .i ki'u bo _Y_} — "_X_, because _Y_"
* {ga je _X_ gi _Y_} — "both _X_ and _Y_"
* {ga ki'u bo _X_ gi _Y_} — "because _X_, _Y_"
* {ga pu bo _X_ gi _Y_} — "before _X_, _Y_"
* {je gi _X_ gi _Y_} — "both _X_ and _Y_"
* {ki'u gi _X_ gi _Y_} — "because _X_, _Y_"
* {pu gi _X_ gi _Y_} — "before _X_, _Y_"

I hope that was useful.
Please let me know if I missed anything or if any of these actually
aren't legal!

.ui ba tavla co'o

[0]: https://vlasisku.lojban.org/bankle
[1]: http://selpahi.weebly.com/lojban/how-to-substantially-simplify-the-lojban-connective-system-my-connective-system
[2]: https://wiki.lojban.io/New_Sentence_Links
[3]: https://discord.com/invite/dGP5A6Fpj7
