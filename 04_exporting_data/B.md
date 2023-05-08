
# Exporting things *other* than tables

## Writing vectors to text file

`writeLines(con='filename.txt')` saves a vector. By default, items are
separated by a newline, i.e. `sep='\n'`. You can separate by other
characters if desired by changing the value of `sep=`:

```R
my_vector <- c(letters,LETTERS)
# Write my_vector to file, one item per line
writeLines(my_vector, con='my_vector.txt')

# Write my_vector as a single comma-separated line
writeLines(my_vector, con='comma_separated.txt', sep=',')
```

Check the contents of the file to confirm it worked as expected.

---

## Saving  R objects as a file

We already mentioned `saveRDS()` and `save()`. Look back
[here](/01_importing_data/B.md) if desired.

---

## On your own
First, generate a vector of 100 random decimals within range (0,1). 
```R
my_numbers <- runif(100)
```
Then use the vector `my_numbers` to answer the following:


Try writing `my_numbers` with `writeLines`. What happens?

<details><summary>Answer</summary>
 
Because `writeLines` only accepts character vectors, it gives an error:
```R
writeLines(my_numbers, con='my_numbers.txt')

Error in writeLines(my_numbers, con = "my_numbers.txt") : 
  can only write character objects
```

</details>

---
How might you get around this limitation to write `my_numbers` to a file?

<details><summary>Answer</summary>
 
 We first have to convert the numeric vector to character with `as.character`
 ```R
 writeLines(as.character(my_numbers), con='my_numbers.txt')
 ```  

</details>

---

[PREV](A.md) | [HOME](/README.md) | [NEXT](C.md)
