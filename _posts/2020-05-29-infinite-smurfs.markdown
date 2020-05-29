---
layout: post
title:  "Infinite Smurfs"
date:   2020-05-29 18:59:00 +0100
categories: riddles smurfs logic compactness infinity
---
So I recently came across an interesting riddle. It comes in two flavors, a
finite version and an infinite version. The first version is well-known and
simply a little bit of a brain teaser, but I hadn't seen the second version
before. That one's not as easy and requires a bit of mathematics.

# Finite Version

Gargamel has captured \\(n\\) smurfs and forces them to participate in a game:
He arranges the smurfs in a line and makes them all face in the same direction.
In particular, the first smurf can see all the other smurfs, the second smurf
can see all other smurfs except the first one, and so on, until finally the
\\(n\\)th smurf can't see any other smurf. For visualization purposes, we set
\\(n = 10\\) below.

\\[s_1 \, s_2 \, s_3 \, s_4 \, s_5 \, s_6 \, s_7 \, s_8 \, s_9 \, s_{10} \\]

Now, Gargamel has devised the following evil scheme: he will put a hat on every
smurf, each one either red or blue, and then he will force the smurfs to guess
the color of their own hat. And he will kill each smurf who gets it wrong!

\\[
    \color{blue} s_1 \,
    \color{red} s_2 \,
    \color{blue} s_3 \,
    \color{blue} s_4 \,
    \color{red} s_5 \,
    \color{blue} s_6 \,
    \color{red} s_7 \,
    \color{red} s_8 \,
    \color{red} s_9 \,
    \color{blue} s_{10}
\\]

Smurf number 1 will have to go first, then smurf number 2, and so on. Of course,
the smurfs cannot see their own hat, but they can see the hats of all the smurfs
in front of them. Moreover, each smurf can hear the answer every other smurf
gives.
Luckily, Gargamel informs the smurfs of these rules before the game starts, so
they have a little time to come up with a plan.

What should the smurfs do to save as many of themselves as possible?

#### Solution

If you gave the puzzle a little thought, you probably came to the conclusion
that \\(s_1\\) is screwed. He has to give an answer without being able to see
his own hat, and nobody answers before him, so he has no way to obtain any
information about his own hat. So for himself, simply flipping a coin would be
as good a strategy as any.
But for the other smurfs, that would be a waste: they wouldn't be able to gather
any information from a random answer.

Instead, \\(s_1\\) should observe the hats of all the other smurfs and base his
answer on that. And indeed, there is the following clever strategy that will
allow all other \\(n - 1\\) smurfs to live: \\(s_1\\) simply counts the number
of blue hats he sees and says *blue* if that number is even, and *red* if it is
odd. By doing so, \\(s_1\\) himself might, of course, die (or live, if the
answer by chance happens to be correct). But what can \\(s_2\\) do
with this information? Let's revisit the example from above:

\\[
    \color{blue} s_1 \,
    \color{red} s_2 \,
    \color{blue} s_3 \,
    \color{blue} s_4 \,
    \color{red} s_5 \,
    \color{blue} s_6 \,
    \color{red} s_7 \,
    \color{red} s_8 \,
    \color{red} s_9 \,
    \color{blue} s_{10}
\\]

Here, \\(s_1\\) sees 4 blue hats: \\(s_3, s_4, s_6\\) and \\(s_{10}\\). As four
is even, \\(s_1\\) will answer *blue*. Now, \\(s_2\\) can also look at the hats
in front of him. And he, too, sees an even number of blue hats. Can he himself
then have a blue hat? No, because if he did, \\(s_1\\) would have seen an odd
number of blue hats, and thus wouldn't have answered *blue*, but *red*.
So \\(s_2\\) can answer *red* and live. By similar reasoning, each smurf can now
successively deduce the color of their own hat.

So we've solved the finite version! That wasn't so hard, was it? Maybe we can
make it a little more tricky.

# Infinite Version
For the second version, the setting is basically the same, only this time,
Gargamel has captured a
[countably infinite](https://en.wikipedia.org/wiki/Countable_set) amount of
smurfs. As markdown doesn't support infinite lists yet, I will only indicate
the beginning of the line:

\\[
    \color{blue} s_1 \,
    \color{red} s_2 \,
    \color{blue} s_3 \,
    \color{blue} s_4 \,
    \color{red} s_5 \,
    \color{blue} s_6 \,
    \color{red} s_7 \,
    \color{red} s_8 \,
    \color{red} s_9 \,
    \color{blue} s_{10}
    \color{black}\dots
\\]

And it's smurfs all the way down. So what can the smurfs do now? The parity
trick from before doesn't work anymore: if there are infinitely many blue hats
in front of you, would you say that that's an even number? Or an odd one?
Neither really makes sense. It seems like the smurfs need a new strategy, one a
little more abstract.

Try to think about it on your own if you want, and then you can check the
solution below.

#### Solution
Observe the following: a smurf can see all of the
infinitely many hats in front of him, and he hears all the answers of the
smurfs behind him. So he has one bit of information for all smurfs except
himself before he has to make a decision. Wouldn't it be nice if this was
enough? Indeed, let's think about these bits as an infinite binary sequence

\\[\alpha \in \\{0, 1\\}^\mathbb{N}\\]

where a 1 represents a (seen or heard) blue hat, and a 0 represents a red hat.
What we want is that for each position \\(n\\), the prefix

\\[\alpha_1, \dots, \alpha_{n - 1}\\]

together with the (infinitely long) suffix

\\[\alpha_{n + 1}, \alpha_{n + 2}, \dots\\]

uniquely determines \\(\alpha_n\\). More formally, we would like to find a
subset of binary sequences \\(S \subseteq \\{0, 1\\}^\mathbb{N}\\) with
the property

\\[
    \forall \alpha, \beta \in \\{0, 1\\}^\mathbb{N}: \alpha \text{ and } \beta
    \text{ differ in exactly one position } \implies
    (\alpha \in S \iff \beta \not\in S)
\\]

In words, we want a set \\(S\\) such that for all pairs of sequences that differ
in exactly one position, exactly one of the two sequences is in \\(S\\). Why do
we want this again? Because when Gargamel picks a sequence \\(\alpha\\) for the
smurfs, the first smurf could look at the tail

\\[\alpha_2, \alpha_3, \dots\\]

and conclude exactly for which \\(\beta_1 \in \\{0, 1\\}\\) the sequence

\\[\beta_1, \alpha_2, \alpha_3, \dots\\]

is contained in \\(S\\). By answering accordingly, he could then let the second
smurf know his hat color, as the answer \\(\beta_1\\) of the first smurf in
conjunction with the tail \\(\alpha_3, \alpha_4, \dots\\) observed by the second
smurf uniquely determines the \\(\beta_2\\) such that the sequence

\\[\beta_1, \beta_2, \alpha_3, \alpha_4, \dots \\]

is in \\(S\\). And as this sequence couldn't differ from

\\[\beta_1, \alpha_2, \alpha_3, \alpha_4, \dots \\]

in exactly one position, we would have \\(\beta_2 = \alpha_2\\), so the
second smurf could save himself. Continued application of this procedure would
save every smurf, except maybe the first one, who again would have to hope that
his answer is correct.

So have we solved the riddle? Well, we have solved it *if* we can find such
a set \\(S\\) satisfying the desirata mentioned above. And that is actually
the hard part of this riddle: proving that such a set \\(S\\) must exist.
For that, we need a little bit of formal logic.