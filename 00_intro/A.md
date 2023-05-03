# Installation and setup

This section goes over how to launch an interactive `R` session in your terminal.

If you are already comfortable doing that on your own, continue to the [NEXT](B.md) section.

*Note: If you are working on a local Linux machine, I assume you already know what you're doing and can get R started on your own*

## A note on `Rstudio`
`Rstudio` is essentially a visual wrapper that goes around the core of `R` and provides additional ways to interface with the program. But everything can be done entirely with text entered at the command-line interface within a terminal (or executed by telling `R` to execute a pre-written text file, or `Rscript`).

While `Rstudio` can be nice, it adds an additional layer of abstraction which can be distracting, or make it less clear exactly what is happening within `R`. For that reason, I'll be using only the console (along with a plain text editor). This console is equivalent to the lower-left window within a typical `Rstudio` setup.

## If you don't have Biowulf access
You should be able to follow along and run the commands within this tutorial in any `R` or `Rstudio` setting so long as the required packages are installed. I'm working in `R` version `4.2.2` with the most recent version of `data.table` and `foreach`.

## Running `R` On Biowulf
Getting started on Biowulf is easy, because it comes with up-to-date versions of `R` and `data.table`/`foreach` preconfigured. After connecting to Biowulf via `ssh`, launch `R` by running:

```bash
sinteractive            # Request an interactive node

# Wait for interactive session to be granted

module load R/4.2       # Load the R 4.2 module
R                       # Start R within the console
```

You should now be working in `R` within the terminal. 

You can suspend your `R` session and access the typical `bash` shell by pressing `[CTRL]`+`[Z]`.

To bring the `R` session back to the foreground, execute the command `fg`

## Libraries

Only `data.table` and `foreach` should be necessary to work through this tutorial.
```R
library(data.table)     # Load data.table
library(foreach)        # Load foreach
```

*Note: `data.table` should be pre-installed within the module on Biowulf. If you *did* need to install the package, it could be done by running `install.packages('data.table')`*

---

[HOME](/README.md) | [NEXT](B.md)