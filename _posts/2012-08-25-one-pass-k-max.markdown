---
layout: post
title: One-pass k-max
tags: puzzles, algorithms
published: false
---

Louis Wasserman posed an interesting question on G+:

    In one pass over a stream of integers, find the top k elements of
    the stream, using O(k) auxiliary storage, O(n+nk) online time, and
    O(k^2) post-processing time.

Note that the one-pass requirement rules out quickselect and heapsort,
and the O(n+nk) requirement rules out a fixed-depth priority queue.

When the runtime is provided, it often leaks a surprising amount of
information.  Here, the O(n + nk) time said I should focus on algorithms
that require only constant work on each element, and I can immediately
dismiss possibility that requires more than O(k) work on each element.

The only integer sort I know whose runtime includes any variable other
than the total element count n is radix sort, so I started there.

First (incorrect) attempt
-------------------------

In pseudo-ML notation, let my state be

    type t = 
    { cutoff : int
    ; buckets :
      { values : int list
      ; len : int
      } array
    }

with the following invariants:

* Every bucket has `len < k`
* In each bucket, all integers share the same prefix in base `r`
* There are `r` buckets, their prefixes differing only in the last digit
* `cutoff` is the largest value 
