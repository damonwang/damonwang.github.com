---
title: "Puzzle: Prefix Reversal"
layout: post
published: false
---

Here's a quick and easy puzzle:

> Given a sequence `S = S[0], ..., S[n-1]` let a prefix reversal 
> `S!m = S[m], S[m-1], ..., S[0], S[m+1], ..., S[n-1]` for all `0 <= m
> <= n` and undefined otherwise.  Sort S using a minimum number of
> prefix reversal operations.

A singleton sequence is trivially already sorted.  Suppose we can sort
any length-`n-1` prefix of a sequence.  Given a length-`n` sequence `S`, 
there exists `i` s.t. for all `s` in `S` we have `S[i] >= s`.  Then
`S!i`  contains all the elements of `S` with its supremum first, and
`S' = S!i!n-1` contains all the elements of `S` with its supremum last.  Once
we recursively sort the first `n-1` elements of `S'` we'll have all the
elements of `S` in sorted order.
