# Setup

I assume you already have access to `R` terminal, `RStudio`, or `Jupyter` notebook.

To retrieve this repository's material by direct download, download this 
[`zip` archive](https://github.com/cory-weller/data-wrangling-R/archive/refs/heads/main.zip)
and unzip the `data-wrangling-R-main` folder into a location you can remember.
You will need to open this target location within `R` or `Rstudio`.

If `git` is installed on your machine (i.e. Mac and linux users):
```bash
# while you are alrady in the directory you want to download to
git clone https://github.com/cory-weller/data-wrangling-R.git
```

---

## A note on `Rstudio`
`Rstudio` is essentially a visual wrapper that goes around the core of
`R` and provides additional ways to interface with the program. But
everything can be done entirely with text entered at the command-line
interface within a terminal (or executed by telling `R` to execute a
pre-written text file, or `Rscript`).

While `Rstudio` can be nice, it does add an additional layer of abstraction 
which can be distracting or make it less clear exactly what is happening
within `R`. This console is equivalent to the lower-left window
within a typical `Rstudio` setup.

You should be able to follow along and run the commands within this
tutorial in any `R` or `Rstudio` setting so long as the required packages
are installed. I most recently tested with `R` version `4.3` with the most recent
version of `data.table` and `foreach`. You will need to manually retrieve
this repository and make sure your `Rstudio` working directory is set
to the top level of said repository.

**Google colab users:** check below for running `R` on Google Colab as a Jupyter notebook

<details><summary>Google Colab setup</summary>

Google offers a free tier of access to its Jupyter notebook platform, 
Colab. While the free tier doesn't come with large memory or computing
resources, it could be a useful tool for learning.

First, while signed in to any Google account, visit the website for
[Google Colab](https://colab.research.google.com)

You'll be greeted with a notebook opening screen. The screen can also
be manually accessed via `File > Open Notebook` on the menu bar.

![](/assets/colab1.png)

To open the one I've prepared to set up `R`, click the `GitHub` tab and
enter the repository info `cory-weller/data-wrangling-R`:

![](/assets/colab2.png)

Then open `R_notebook.ipynb`. You'll then be taken to the notebook
interface, which is composed of cells of text or code. Cells of code
must be ran by either clicking the play button, or pressing the keys
`CTRL`+`ENTER` while the cell is selected.

![](/assets/colab3.png)

Because I authored the notebook (and not Google), you'll see a warning
to make sure you trust the contents before continuing. You can see for
yourself that the cell only does the following:
* installs the `rpy2` utility (which lets us interface with `R` in the notebook)
* loads `rpy2`
* Installs three R packages

The 'play' button next to the cell will change to runnning state, with
a 'stop' button if you want to halt execution.

Once the code within the cell is finished running (there will be some
warnings printed during the installation), the button will change back
to the 'play' icon, and a green checkmark will be shown.

Scroll down and note that Jupyter uses *cell magic* to indicate when
to run different coding languages. By default, the cell will run as
`python` code. To tell the notebook to instead use `R`, begin that
cell with `%%R`. There are two final considerations:

* First, know that your notebook session is ephemeral! If you walk away or
close the session, the state of the machine hosting the notebook will
power off, and all code will need to be re-ran the next time you connect.
* Second, because you are opening up a copy of the notebook from GitHub,
you will need to save the notebook to your own google account for any
changes to be saved. Otherwise your work will be lost. You can save
your own copy via `File > Save a Copy in Google Drive`.


</details>



---

## Running `R` On Biowulf
Getting started on Biowulf is easy, because it comes with up-to-date
versions of `R` and `data.table`/`foreach` preconfigured. Note that
you must request an interactive node before you can run `R`. After you
connect to Biowulf via `ssh`, run the following:

```bash
sinteractive            # Request an interactive node

# Wait for interactive session to be granted

module load R/4.2       # Load the R 4.2 module
R                       # Start R within the console
```

You should now be working in `R`. 

You can suspend your `R` session and access the typical `bash` shell
by pressing `[CTRL]`+`[Z]`. This is often handy when you need to
quickly run some `bash` commands before going back to `R`.

To bring the `R` session back to the foreground, execute the command `fg`

---

## Libraries

Only `data.table` and `foreach` should be necessary to work through
this tutorial.
```R
library(data.table)     # Load data.table
library(foreach)        # Load foreach
```

*Note: `data.table` should be pre-installed within the module on Biowulf.*
If you *did* need to install the package, it could be done by running 
the command (within `R`) `install.packages('data.table')`

---

[PREV](/00_intro/README.md) | [HOME](/README.md) | [NEXT](B.md)