# Importing R data objects

Sometimes you want to load (or save) `R` objects exactly as they appear in your current session, instead of outputting to text.
This can be done by writing a binary representation of your object (or objects) to the disk. A single R object can be saved with `saveRDS`:

```R
saveRDS(mydataobject, file='mydata.rds')

# later...
mydataobject <- readRDS('mydata.rds')
```
The `.rds` file is a binary compressed representation of the object, meaning it cannot be read as text--it needs to be loaded by `R` to convert back into its original representation.

Note that `readRDS` doesn't know the original name of the object, so you need to re-assign it to some variable name. 

Multiple objects can be written to the disk with `save`, with `save.image` being a special case that saves  all objects in your session to be restored later.

```R
save.image('mysession.Rdata')

# later...
load('mysession.Rdata')
```
The original variable names stored in the `.Rdata` file will automatically be loaded along with their contents. Note that any packages will need to be loaded again if it's a new R session!

---

[PREV](B.md) | [HOME](/README.md) | [NEXT](/02_filtering_data/README.md)
