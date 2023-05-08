# Iterating with `foreach`

**Note**: here, I assume you are familiar with `for` loops in `R`. If
not, or if you need a refresher, check [this out](https://intro2r.com/loops.html).


The `foreach` function is a superpowered replacement to `for`. The
important differences are:
* `foreach` returns a `data.table` for each iteration
* `foreach` can efficiently perform all iterations in parallel,
saving computation time

As such, use `foreach` when you want to do a calculation or summarize
some statistic in a loop. But **don't** use `foreach` if you want to
add or modify any data in the tables being analyzed.

---

[PREV](README.md) | [HOME](/README.md) | [NEXT](A.md)
