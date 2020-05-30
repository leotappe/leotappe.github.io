---
layout: post
title:  "Infinite Smurfs"
date:   2020-05-30 10:00:00 +0100
categories: riddles smurfs logic compactness infinity
---
So I recently came across an interesting riddle. It comes in two flavors, a
finite version and an infinite version. The first version is well-known and
simply a little bit of a brain teaser, but I hadn't seen the second version
before. That one's not quite as easy and requires a bit of mathematics.

# Finite Version

Gargamel has captured \\(n\\) smurfs and forces them to participate in a game:
He arranges the smurfs in a line and makes them all face in the same direction.
In particular, the first smurf can see all the other smurfs, the second smurf
can see all other smurfs except the first one, and so on, until finally the
\\(n\\)th smurf can't see any other smurf. For visualization purposes, we set
\\(n = 10\\) below.

\\[\overrightarrow{s_1 \, s_2 \, s_3 \, s_4 \, s_5 \, s_6 \, s_7 \, s_8 \, s_9 \, s_{10}} \\]

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

#### Solution (Part 1/2)
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
subset of binary sequences \\(A \subseteq \\{0, 1\\}^\mathbb{N}\\) with
the property

\\[
    \forall \alpha, \beta \in \\{0, 1\\}^\mathbb{N}: \alpha \text{ and } \beta
    \text{ differ in exactly one position } \implies
    (\alpha \in A \iff \beta \not\in A)
\\]

In words, we want a set \\(A\\) such that for all pairs of sequences that differ
in exactly one position, exactly one of the two sequences is in \\(A\\). Why do
we want this again? Because when Gargamel picks a sequence \\(\alpha\\) for the
smurfs, the first smurf could look at the tail

\\[\alpha_2, \alpha_3, \alpha_4, \dots\\]

and conclude exactly for which \\(\beta_1 \in \\{0, 1\\}\\) the sequence

\\[\beta_1, \alpha_2, \alpha_3, \alpha_4, \dots\\]

is contained in \\(A\\). By answering accordingly, he could then let the second
smurf know his hat color, as the answer \\(\beta_1\\) of the first smurf in
conjunction with the tail \\(\alpha_3, \alpha_4, \dots\\) observed by the second
smurf uniquely determines the \\(\beta_2\\) such that the sequence

\\[\beta_1, \beta_2, \alpha_3, \alpha_4, \dots \\]

is in \\(A\\). And as this sequence couldn't differ from

\\[\beta_1, \alpha_2, \alpha_3, \alpha_4, \dots \\]

in exactly one position, we would have \\(\beta_2 = \alpha_2\\), so the
second smurf could save himself. Continued application of this procedure would
save every smurf, except maybe the first one, who again would have to hope that
his answer is correct.

So have we solved the riddle? Well, we have solved it *if* we can find such
a set \\(A\\) satisfying the desirata mentioned above. And that is actually
the hard part of this riddle: proving that such a set \\(A\\) must exist.

#### Solution (Part 2/2)

The existence of \\(A\\) is not obvious. We could try a constructive approach,
but this would likely soon fail. Instead, the problem lends itself naturally to
the language of propositional logic. Essentially, we need to make
a binary decision for every \\(\alpha \in \\{0, 1\\}^\mathbb{N}\\): do we
include it in \\(A\\) or not? So let these decision variables be our set of
propositonal variables

\\[X = \\{x_\alpha \mid \alpha \in \\{0, 1\\}^\mathbb{N}\\} \\]

Note that this already is an
[uncountably large](https://en.wikipedia.org/wiki/Uncountable_set) amount of
propositional variables! An assignment to these variables will then induce a
set \\(A\\) by simply including those \\(\alpha\\) in \\(A\\) for which
\\(x_\alpha\\) is set to 1.

Okay, now that we have the variables, we need some formulas. In particular,
we need to encode the constraint that for each pair of sequences that differ in
exactly one position, exactly one of them is included in \\(A\\). So if
\\(\alpha\\) and \\(\beta\\) are two such sequences, this can be expressed with
the formula

\\[
    F_{\alpha, \beta} = (x_\alpha \lor x_\beta) \land
    (\lnot x_\alpha \lor \lnot x_\beta)
\\]

And now, the existence of the desired set \\(A\\) is equivalent to the
satisfiability of the (uncountably large) set of formulas

\\[\mathcal{S} = \\{F_{\alpha, \beta} \mid \alpha \text{ and } \beta 
\text{ differ in exactly one position}\\}\\]

At first glance, it doesn't seem like we've made much progress. How would we
know whether an infinite set of formulas is satisfiable? Fortunately, some
clever logicians already came up with the
[compactness theorem](https://en.wikipedia.org/wiki/Compactness_theorem),
which states the following:

> A set of formulas is satisfiable if and only if every finite subset of it
> is satisfiable.

Aha! This lets us reason about the infinite set \\(\mathcal{S}\\) in terms of
its finite subsets. We now only have to prove that every finite subset
\\(\mathcal{T} \subset \mathcal{S}\\) is satisfiable. So why is this the
case? Well, notice that any such finite subset corresponds to a formula in
[2-CNF](https://en.wikipedia.org/wiki/2-satisfiability): each clause consists
of exactly two literals. And luckily, there is a nice characterization of
satisfiability for 2-CNF formulas: Precisely those 2-CNF formulas are satisfiable
whose implication graph is consistent. What does this mean? It means that if you
construct the graph whose nodes are the literals of the formula, and you
introduce for each clause of literals \\(L_1 \lor L_2\\) the directed edges
\\(\overline{L_1} \rightarrow L_2\\) and
\\(\overline{L_2} \rightarrow L_1\\), that then no literal \\(L\\) is in the
same
[strongly connected component](https://en.wikipedia.org/wiki/Strongly_connected_component)
as its negation \\(\overline{L}\\).

Phew, that's a lot to take in, but we're almost there: we just need to give 
an argument why any finite subset of \\(\mathcal{S}\\) corresponds to a 2-CNF
formula with a consistent implication graph. So let's take a look at what such
an implication graph looks like in our case. Our formulas are all of the
form

\\[
    (x_\alpha \lor x_\beta) \land
    (\lnot x_\alpha \lor \lnot x_\beta)
\\]

So we have the following edges in our graph:

\\[
    \lnot x_\alpha \rightarrow x_\beta \newline
    \lnot x_\beta \rightarrow x_\alpha \newline
    x_\alpha \rightarrow \lnot x_\beta \newline
    x_\beta \rightarrow \lnot x_\alpha
\\]

Notice that all edges go between positive literals and negative literals,
never between two positive literals or two negative literals. So can it be
that the implication graph is inconsistent? This would imply that there
is a path from a variable \\(x_\alpha\\) to its negation \\(\lnot x_\alpha\\).
By our observation from above that each edge goes between a negative and
a positive variable, such a path would have to have odd length. Furthermore,
we only have edges between variables that correspond to sequences that differ
in exactly one position. So each step in a path changes exactly one position
of the sequence, and thus an odd path would correspond to an odd number of
changes. But this means it is impossible for there to be a path
\\(x_\alpha \rightsquigarrow \lnot x_\alpha\\), as an odd number of changes
can never return the sequence \\(\alpha\\) back to itself. We can conclude
that the implication graph must be consistent. And as this holds for
every finite subset of \\(\mathcal{S}\\), by the compactness theorem,
\\(\mathcal{S}\\) must be satisfiable, and hence, the desired set must exist.

And that's it! We have found a way to save all but possibly one smurf: simply
pick a suitable set \\(A\\) (the existence of which we're now sure of) and
follow the strategy outlined above.