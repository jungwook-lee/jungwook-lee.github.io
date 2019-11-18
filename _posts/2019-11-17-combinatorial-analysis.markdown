---
layout: single
title:  "Learn Probability Day 1: Combinatorial Analysis"
date:   2019-11-17 10:40:00 -0400
categories: probability basics
---

Combinatorial Analysis is a fancy way of counting! It is useful to know how to count the number of ways in which events can occur. Why manually count each possible outcomes, when you can simply use a formula?

**The Basic Principle of Counting**: For 2 independent events, if event 1 has \\(m\\) possible outcomes, and event 2 has \\(n\\) possible outcomes, then there are total of \\(m \cdot n\\) outcomes possible for two events.

**Generalized Basic Principle of Counting**: If there are \\(r\\) experiments such that \\(r_1\\) has \\(n_1\\) possible outcomes and there are \\(n_2\\) for the second experiment and so on; then there is a total of \\(n_1 \cdot n_2 \cdot ... \cdot n_r\\) possible outcomes.

**Permutations**: Possible arrangement of n items.

\\[ n! = n(n - 1)(n - 2) ... (3)(2)(1) \\]

In general, if there are alike items in the set, their permutation can be eliminated in the total possibilities. For permutation of \\(n\\) items with \\( n_1, n_2 \ldots n_r \\) alike items:

\\[ \frac{n!}{n_1!, n_2! \ldots n_r!} \\]

**Generalized Permuatation**: \\(n\\) is the number of items, land \\(k\\) is the number of permutation length.

\\[ _nP_k = \frac{n!}{(n - r)!}\\] 

**Combinations**: Number of possible groups of \\(r\\) objects that can be formed with total \\(n\\) objects. Note that \\( n \leq r\\).

\\[ _nC_k = \binom{n}{k} = \frac{n!}{r!(n - r)!} \\] 

The above equation is used often in binomial theorem.