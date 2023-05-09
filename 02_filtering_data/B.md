# Extracting by conditions

While specifying rows is simple, it would be tedious to manually define
which rows we want to keep, and then run the operation in `R`. Instead,
it's common to filter rows such that certain *conditions* must be met.

Still working with the example `data.table` from before:
```R
dat <- data.table('N'=1:26, 'lower'=letters, 'upper'=LETTERS)
```

We can use a filter within `i` instead of a vector of indices. `R` will
automatically subset rows where that condition is `TRUE`.

Run the following commands and evaluate the results:
```R
dat[N < 10]
dat[N >= 15]

# The %% (modulo) operator returns the remainder after division
dat[N %% 2 == 0]        
dat[lower == 'a']
dat[lower == 'A']
```

We can include conditional operators within these tests:
* indicate AND with `&`
* indicate OR with `|` (`SHIFT` + key above `RETURN`)
* indicate NOT with `!`
* indicate EQUALS with `==`
* indicate NOTEQUAL with `!=`

```R
dat[N < 10 & lower != 'c']
```

Additionally, the greater/less than (and their or-equal-to counterparts)
`>`, `<`, `>=` and `<=` work here.

Note: Assigning new variables can be done with `=` or with `<-`. 

It is advisable to avoid using `=` to reduce confusion with `==`


---
## On your own

How would you use a conditional filter to subset only rows with odd
values of `N`?[^1]

<details><summary>Answer</summary>
 
```R
dat[N %% 2 != 0]
```

</details>



---
How would you subset only rows with `upper` in the set `N`, `I` and `H` ?
<details><summary>Answer</summary>

```R
dat[upper == 'N' | upper == 'I' | upper == 'H']
```

</details>

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)


[^1]: Recall the `remainder` function `%%`