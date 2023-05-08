# Why `data.table`? What about `dplyr`?

In the memory and speed benefits of `data.table` were very valuable
when working with millions of iterations of extremely large data sets.
However, very large data may not be typical in one's workflow. When
working with reasonably sized data (i.e. up to single digit Gigabytes
of data in memory), differences in efficiency shouldn't matter much. 
* Chaining syntax
* It's what I know best


After trying `data.table` you might become a convert. But even if you
don't, the techniques described here should still be useful, or even
directly applicable to `dplyr`. While AI hasn't fully taken over our
jobs yet, it is quite proficient at converting `data.table` notation
into `dplyr` notation. 

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)
