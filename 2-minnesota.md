---
editor_options: 
  markdown: 
    wrap: 72
---

::: {#quarto-search-results}
:::

:::::::: {#quarto-header .headroom .fixed-top}
::::::: {.navbar-container .container-fluid}
::: {.navbar-brand-container .mx-auto}
[![](../csu-rams-logo.png){.navbar-logo}](../index.html){.navbar-brand
.navbar-brand-logo} [[ESS
330](../index.html){.navbar-brand}]{.navbar-title}
:::

::: {#quarto-search title="Search"}
:::

::: {#navbarCollapse .collapse .navbar-collapse}
-   [[Home](../index.html){.nav-link}]{.menu-text}
-   [[Syllabus](../syllabus.html){.nav-link}]{.menu-text}
-   [[Schedule](../schedule.html){.nav-link}]{.menu-text}
-   [[Labs](../labs.html){.nav-link}]{.menu-text}

<!-- -->

-   
:::

::: quarto-navbar-tools
[ ](%22Toggle%20dark%20mode%22){.quarto-color-scheme-toggle
.quarto-navigation-tool .px-1
onclick="window.quartoToggleColorScheme(); return false;"}
:::
:::::::
::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {#quarto-content .quarto-container .page-columns .page-rows-contents .page-layout-article .page-navbar}
::: {#quarto-margin-sidebar .sidebar .margin-sidebar}
## On this page {#toc-title}

-   [Intro to `dplyr`:](#intro-to-dplyr){#toc-intro-to-dplyr .nav-link
    .active scroll-target="#intro-to-dplyr"}
    -   [Key Features of
        dplyr](#key-features-of-dplyr){#toc-key-features-of-dplyr
        .nav-link scroll-target="#key-features-of-dplyr"}
    -   [Dataset](#dataset){#toc-dataset .nav-link
        scroll-target="#dataset"}
        -   [Piping](#piping){#toc-piping .nav-link
            scroll-target="#piping"}
-   [Minnesota tree growth
    data:](#minnesota-tree-growth-data){#toc-minnesota-tree-growth-data
    .nav-link scroll-target="#minnesota-tree-growth-data"}
-   [Exercises](#exercises){#toc-exercises .nav-link
    scroll-target="#exercises"}
    -   [1. Filtering rows](#filtering-rows){#toc-filtering-rows
        .nav-link scroll-target="#filtering-rows"}
    -   [2. Slicing rows](#slicing-rows){#toc-slicing-rows .nav-link
        scroll-target="#slicing-rows"}
    -   [3. Arranging Rows](#arranging-rows){#toc-arranging-rows
        .nav-link scroll-target="#arranging-rows"}
    -   [4. Reducing Columns](#reducing-columns){#toc-reducing-columns
        .nav-link scroll-target="#reducing-columns"}
    -   [5. Renaming columns](#renaming-columns){#toc-renaming-columns
        .nav-link scroll-target="#renaming-columns"}
    -   [6. Creating new
        columns](#creating-new-columns){#toc-creating-new-columns
        .nav-link scroll-target="#creating-new-columns"}
    -   [7. case_when /
        if_else](#case_when-if_else){#toc-case_when-if_else .nav-link
        scroll-target="#case_when-if_else"}
    -   [8. Summarizing](#summarizing){#toc-summarizing .nav-link
        scroll-target="#summarizing"}
    -   [9. Grouped data](#grouped-data){#toc-grouped-data .nav-link
        scroll-target="#grouped-data"}
        -   [How do `dplyr` functions behave given a grouped
            `data.frame`?](#how-do-dplyr-functions-behave-given-a-grouped-data.frame){#toc-how-do-dplyr-functions-behave-given-a-grouped-data.frame
            .nav-link
            scroll-target="#how-do-dplyr-functions-behave-given-a-grouped-data.frame"}
    -   [10. Counting](#counting){#toc-counting .nav-link
        scroll-target="#counting"}
-   [Final Question:](#final-question){#toc-final-question .nav-link
    scroll-target="#final-question"}
-   [Rubric](#rubric){#toc-rubric .nav-link scroll-target="#rubric"}
:::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {#quarto-document-content .content role="main"}
::::: {#title-block-header .quarto-title-block .default}
::: quarto-title
# Lab 2: Minnesota tree growth {#lab-2-minnesota-tree-growth .title}

Manipulating and summarizing data with dplyr
:::

::: quarto-title-meta
:::
:::::

::::: cell
:::: cell-output-display
<div>

<figure class="figure">

<p><img src="images/minn-forest.jpg" class="img-fluid figure-img" width="1518"/></p>

</figure>

</div>
::::
:::::

:::::::::::::::::::::::: {#intro-to-dplyr .section .level1}
# Intro to `dplyr`:

:::: cell
::: {#cb1 .sourceCode .cell-code}
``` {.sourceCode .r .code-with-copy}
library(dplyr)
```
:::
::::

::::: cell
:::: cell-output-display
<div>

<figure class="figure">

<p><img src="../slides/images/dplyr.jpg" class="img-fluid figure-img" width="600"/></p>

</figure>

</div>
::::
:::::

`dplyr` is an R package that provides a set of functions designed for
data manipulation and transformation, making it easier to work with data
frames (or tibbles). It is part of the tidyverse ecosystem and is widely
used for data wrangling tasks such as filtering, selecting, summarizing,
and mutating data.

:::::: {#key-features-of-dplyr .section .level2}
## Key Features of dplyr {.anchored anchor-id="key-features-of-dplyr"}

1.  **Pipe-friendly** (`%>%`/`|>`): Works seamlessly with the pipe
    operators.
2.  **Efficient**: Built on top of Rcpp for fast performance.
3.  **Consistent Grammar**:Uses a consistent set of verbs for data
    manipulation.

The primary verbs can be organized into three categories based on the
component of the dataset they most commonly operate on:

::: {#rows .section .level4}
#### Rows: {.anchored anchor-id="rows"}

-   `filter()`: subset rows based on column values.
-   `slice()`: subset rows based on index.
-   `arrange()`: change row order.
:::

::: {#columns .section .level4}
#### Columns: {.anchored anchor-id="columns"}

-   `select()`: subset columns based on name or characteristics.
-   `mutate()`: change column values or create new columns.
-   `rename()`: change column name.
:::

::: {#groups-of-rows .section .level4}
#### Groups of rows: {.anchored anchor-id="groups-of-rows"}

-   `summarize()`: collapse multiple rows into a single row.
-   `n()`/`n_distint()`: count group membership
:::
::::::

:::::::::::::: {#dataset .section .level2}
## Dataset {.anchored anchor-id="dataset"}

-   `glimpse()` provides a compact and easy-to-read summary of a
    data.frame. It is similar to `str()`, but with a more readable
    format. Its key features are that it:

We will use glimpse to report on our outputs in each question through
this lab!

::::::::::::: {#piping .section .level3}
### Piping {.anchored anchor-id="piping"}

The pipe operator (`|>`) in R is used to streamline code by passing the
result of one function directly into the next function as the *first
argument*.

-   Base R Pipe (`|>`): Introduced in R 4.1.0, the native pipe works
    similarly to the magrittr pipe (%\>%) but is built into base R.

-   Tidyverse Pipe (%\>%): allows greater flexibility than `|>`, such as
    using placeholders (.) when the first argument isn't where the
    function expects input and automatically handling non-standard
    evaluation in dplyr. Must be loaded with `dplyr`/`magrittr`

:::::::::::: {#key-differences .section .level4}
#### Key Differences {.anchored anchor-id="key-differences"}

| Feature | `|>` (Base R) | `%>%` (Tidyverse) |
|:------------------|:----------------------|:-----------------------------|
| Available in | R 4.1.0+ (no extra packages) | {magrittr} package |
| First argument | Always passed as first argument | Can use . for flexibility |
| Function compatibility | Works with most functions | Works better with dplyr and NSE functions |

**Example 1: Without Pipe**

::::: cell
::: {#cb2 .sourceCode .cell-code}
``` {.sourceCode .r .code-with-copy}
round(mean(c(1, 2, 3, 4, 5), na.rm = TRUE), digits = 2)
```
:::

::: {.cell-output .cell-output-stdout}
```         
[1] 3
```
:::
:::::

**Example 2: Using native pipe \|\>**

::::: cell
::: {#cb4 .sourceCode .cell-code}
``` {.sourceCode .r .code-with-copy}
c(1, 2, 3, 4, 5) |> 
  mean(na.rm = TRUE) |> 
  round(digits = 2)
```
:::

::: {.cell-output .cell-output-stdout}
```         
[1] 3
```
:::
:::::

**Example 3: Using %\>% pipe**

::::: cell
::: {#cb6 .sourceCode .cell-code}
``` {.sourceCode .r .code-with-copy}
c(1, 2, 3, 4, 5) %>% 
  mean(na.rm = TRUE) %>%  
  round(digits = 2)
```
:::

::: {.cell-output .cell-output-stdout}
```         
[1] 3
```
:::
:::::

If you're using `tidyverse`/`dplyr`, `%>%` is still widely used. If
you're sticking to base R, `|>` is the better choice.
::::::::::::
:::::::::::::
::::::::::::::
::::::::::::::::::::::::

::: {#minnesota-tree-growth-data .section .level1}
# Minnesota tree growth data:

To start this lab, create a new Rproj with the proper structure (docs,
images, data) and create a copy of this quarto file in it.

This lab is centered around exploring data manipulation with `dplyr`
using a long term tree growth observation record from Minnisota. The
Minnesota tree growth dataset can be found as part of the paper
[Variable effects of climate on forest growth in relation to climate
extremes, disturbance, and forest
dynamics](https://site.uvm.edu/tdamato/files/2021/05/Itter-et-al.-2017-EC-APPS.pdf).
As with most (good) papers, a data availability statement at the end of
this paper tells us the data used in the study can be found on
[Dyrad](https://datadryad.org/stash/dataset/doi:10.5061/dryad.18pm5).
From the attached `README` we see the following data description:

`tree_dat.csv` -- Annual radial growth increments for individual trees.
Variables included in the tree data set are as follows.

-   **treeID**: unique tree identifier (total of 2,291 trees)\

-   **standID**: unique stand identifier (total of 35 stands)\

-   **stand**: alpha-numeric stand code\

-   **year**: year of growth (study period equals 1897 to 2007)\

-   **species**: species code (15 unique species, see below)\

    | Symbol | Species               |
    |:-------|:----------------------|
    | ABBA   | Abies balsamea        |
    | ACRU   | Acer rubrum           |
    | ACSA   | Acer saccharum        |
    | BEPA   | Betula papyrifera     |
    | FRNI   | Fraxinus nigra        |
    | LALA   | Larix laricina        |
    | PIBA   | Pinus banksiana       |
    | PIGL   | Picea glauca          |
    | PIMA   | Picea mariana         |
    | PIRE   | Pinus resinosa        |
    | PIST   | Pinus strobus         |
    | POGR   | Populus grandidentata |
    | POTR   | Populus tremuloides   |
    | QURU   | Quercus rubra         |
    | THOC   | Thuja occidentalis    |

-   **age**: age of tree during year of growth\

-   **inc**: linear growth increment (mm)\

-   **rad_ib**: estimated inside bark radius of tree at breast height at
    the end of the year of grow (mm)\

Go to the above Dyrad site, and download this data sticking it into your
data directory (unzipped).
:::

::::::::::::::::::::::::::::: {#exercises .section .level1}
# Exercises

:::::: {#filtering-rows .section .level2}
## 1. Filtering rows {.anchored anchor-id="filtering-rows"}

`filter()` creates row subsets that satisfy a condition involving values
in one or more columns. The first argument in `filter()` is the
`data.frame` from which you want to subset rows. Conditional statements
passed as separate arguments are combined with the & operator.

::::: cell
:::: cell-output-display
<div>

<figure class="figure">

<p><img src="images/02-filter.jpeg" class="img-fluid figure-img" width="2048"/></p>

</figure>

</div>
::::
:::::

For this lab, you will read in the Minnesota tree growth dataset from
the `trees_dat.csv` file found from Dyrad and saved to your `data`
folder.

> **Question 1: Read in the Minnesota tree growth dataset. Use `glimpse`
> to understand the structure and names of the dataset. Decribe the
> structure and what you see in the dataset?**
>
> ``` r
> tree <-read.csv("data/tree_dat.csv") glimpse(tree)
> ```
>
> There are 8 columns and 131,386 rows. Each tree in the study is
> cataloged by stand, species, and observations are made by year. The
> age of the tree is given, and the rest of this information can be
> found in the README of the dataset.

> **Question 2: How many records have been made in stand 1?**
>
> ``` r
> stand_count <- tree %>%  + filter(standID == 1) %>%  + count()
> ```
>
> There are 979 observations in stand 1.

> **Question 3: How many records of the Abies balsamea and Pinus strobus
> species have been made?**
>
> > abies_pinus \<- tree %\>% + filter(species %in% c("ABBA", "PIST"))
> > nrow(abies_pinus) [1] 17221
>
> ``` r
> 17221 records
> ```

> **Question 4: How many trees are older then 200 years old in the last
> year of the dataset?**
>
> ```         
>  tree %>%  + filter(year == max(year), age > 200) 
> ```

there are 7 trees older than 200 years from 2007
::::::

::: {#slicing-rows .section .level2}
## 2. Slicing rows {.anchored anchor-id="slicing-rows"}

You can use the `slice()` family of functions to extract a chunk of your
rows by their position in the dataset.

This function family includes:

`slice(X:Y)`: filters out rows X to Y (where X and Y are numbers).
`slice_max / slice_min` - filters for observations with the max/min
values for a variable V. `slice_head`/`slice_tail` - return the first
and last row of the given data.frame, respectively `slice_sample` -
return a random subset of rows, with or without replacement, and with
specified selection probability

```         
 tree %>%  + arrange(-age) %>%  + slice_head(n=5)   
```

Change the n argument in these functions to return more than one row
(i.e., the default argument is n = 1), or use the prop argument to
return the desired proportion of rows.

> **Question 5: What is the oldest tree in the dataset found using
> slice_max?**
>
> ```         
> > tree %>%  + slice_max(age)
> ```

> 269 years
>
> **Question 6: Find the oldest 5 trees recorded in 2001. Use the help
> docs to understand optional parameters**
>
> ```         
> > tree %>% 
> + filter(year == 2001) %>% 
> + arrange(-age) %>% 
> + slice_head(n=5)
>
> | treeID| standID| age|
> |------:|-------:|---:|
> |     24|       2| 263|
> |     25|       2| 259|
> |   1595|      24| 212|
> |   1598|      24| 206|
> |   1712|      26| 206|
> ```

> **Question 7: Using slice_sample, how many trees are in a 30% sample
> of those recorded in 2002?**

```         
```

There are 687 observed trees
:::

::: {#arranging-rows .section .level2}
## 3. Arranging Rows {.anchored anchor-id="arranging-rows"}

`arrange()` orders rows based on values in one or more columns. If you
specify more than one column, each additional column is used to break
ties in values of preceding columns. The default behavior is to sort
column values in **ascending** order (i.e., smallest values at the top).
If you want to sort column values in descending order, put the column
name inside \*\*desc(*)*.

`arrange()` doesn't change the number of rows, only their order. Row
order doesn't typically matter when analyzing data; however, order is
often important for understanding and communicating data structure.

> **Question 8: Filter all trees in stand 5 in 2007. Sort this subset by
> *descending* radius at breast height (rad_ib) and use slice_head() to
> get the top three trees. Report the tree IDs**

```         
```
:::

| treeID |   rad_ib | age |
|-------:|---------:|----:|
|    128 | 238.8850 |  82 |
|    157 | 217.8700 |  85 |
|    135 | 210.1874 |  84 |

The top three trees are tree 128; 238.8850 mm, Tree 157; 217.8700 mm,
Tree 135; 210.1874 mm.

::: {#reducing-columns .section .level2}
## 4. Reducing Columns {.anchored anchor-id="reducing-columns"}

Another common task is to select a subset of columns in the dataset.
This is accomplished using `select()`.

> **Question 9: Reduce your full `data.frame` to**
> $$treeID, stand, year,
> and radius at breast height$$. Filter to only those in stand 3 with
> records from 2007, and use slice_min to pull the smallest three trees
> measured that year.

> | treeID | standID | year | rad_ib |
> |-------:|--------:|-----:|-------:|
> |     50 |       3 | 2007 | 47.396 |
> |     56 |       3 | 2007 | 48.440 |
> |     36 |       3 | 2007 | 54.925 |
>
> ``` r
> >smallest3_07 <- tree %>% 
> + select(treeID, standID, year, rad_ib) %>% 
> + filter(year == 2007, standID == 3) %>% 
> + slice_min(order_by = rad_ib, n = 3)
> ```
>
> **Question 10: Use select to *remove* the stand column. Use glimspe to
> show the dataset.**
>
> glimpse(tree %\>% select(!stand))
>
> Rows: 131,386 Columns: 7

> **Question 11: Look at the help document for dplyr::select and examine
> the "Overview of selection features". Identify an option (there are
> multiple) that would help select all columns with the string "ID" in
> the name. Using glimpse to view the remaining dataset**

The `&` and `|` operators provide additional flexibility for specifying
columns to retain or exclude. Use `&` to identify the intersection
between two column sets (i.e., those columns that are in both sets). Use
`|` to identify the union of two column sets (i.e., all columns in at
least one set).

use ends_with()

ex:

``` r
ID_columns <-(tree %>% select(ends_with("ID")))
glimpse(ID_columns)

Rows: 131,386
Columns: 2

```

> **Question 12: Find a selection pattern that captures all columns with
> either 'ID' or 'stand' in the name. Use glimpse to verify the
> selection.**
>
> ``` r
> glimpse(tree %>% select(ends_with("ID"), starts_with("stand")))
>
> Rows: 131,386 Columns: 3
> ```
:::

:::::: {#renaming-columns .section .level2}
## 5. Renaming columns {.anchored anchor-id="renaming-columns"}

It's easy to rename data.frame columns using rename(). The first
argument in rename() is the data.frame containing columns to rename and
subsequent arguments takes the form new_name = old_name.

::::: cell
:::: cell-output-display
<div>

<figure class="figure">

<p><img src="../slides/images/rename.png" class="img-fluid figure-img" width="1920"/></p>

</figure>

</div>
::::
:::::

> **Question 13: Looking back at the data dictionary, rename rad_inc and
> inc to include `_[unit]` in the name. Unlike earlier options, be sure
> that this renaming is permanent, and stays with your data.frame
> (e.g. `<-`). Use glimpse to view your new data.frame.**

``` r
tree_mod <- tree %>%  + rename(rad_ib_mm = rad_ib, growth_inc_mm = inc)
glimpse(tree_mod)
Rows: 131386
Columns: 8
```
::::::

:::::: {#creating-new-columns .section .level2}
## 6. Creating new columns {.anchored anchor-id="creating-new-columns"}

`mutate()` creates new columns (or modifies existing ones) and adds them
to the right side of an existing `data.frame`. The first argument in
`mutate()` is the `data.frame` to be augmented and subsequent arguments
define the new columns. This function is useful because exiting columns
in the `data.frame` can be referenced when defining new columns.

::::: cell
:::: cell-output-display
<div>

<figure class="figure">

<p><img src="../slides/images/dplyr_mutate.jpg" class="img-fluid figure-img" width="600"/></p>

</figure>

</div>
::::
:::::

> **Question 14: A key measurement in forestry in "basal area column".
> The metric is computed with the formula:\
> BA(m2) = 0.00007854⋅DBH\^2\
> Where DBH is the diameter at breast height (cm). Use mutate to compute
> DBH in centimeters, and BA in m2 (HINT: Make sure rad_ib is in cm
> prior to computing the diameter!). What is the mean BA_m2 of the the
> species `POTR` in 2007?**
>
> ```         
> tree_mutate <- tree_mod %>%  +     mutate(dbh = rad_ib_mm*10) %>%  +     mutate(ba_m2 = dbh^2*.00007854)
>
> > tree_mutate %>% 
> +     filter(year == 2007, species == "POTR") %>% 
> +     summarize(ba_m2_07 = mean(ba_m2, na.rm = TRUE))
>   ba_m2_07
> ```

The mean basal area for aspen in 2007 was .00924156 m\^2.
::::::

::::::: {#case_when-if_else .section .level2}
## 7. case_when / if_else {.anchored anchor-id="case_when-if_else"}

Many times the values we want to assign a new column using `mutate()`
are conditional on the values in other columns. One approach is to use
the dplyr's `if_else()` function, which is defined as
`if_else(condition, true, false, missing = NULL)`, where condition is a
logical vector created using one or more vectors and logical operators.

> **Question 15: Lets say for the sake of our study, trees are not
> established until they are 5 years of age. Use `if_else` to add a
> Boolean column to our data set called `established` that is TRUE if
> the age is greater then 5 and FALSE if less then or equal to five.
> Once added, use count (see ?count) to determine how many records are
> from established trees.**

``` r
 tree <- tree %>% 
  mutate(is_old = if_else(age >= 5, TRUE, FALSE))
  count(tree_old)
```

| tree_old |      n |
|:---------|-------:|
| FALSE    |   6951 |
| TRUE     | 124435 |

There are 124,435 records from established trees.

```         

  tree_old      n 1    FALSE   6951 2     TRUE 124435
```

`case_when()` provides a vectorized way to apply multiple conditional
statements. It is commonly used for creating new variables based on
conditions. *In `case_when()`, each condition is evaluated in order, and
the first one that is TRUE determines the output. `case_when()`* takes
one or more arguments, where each argument, is a two-sided formula where
the left side is separated by the right side by a tilde symbol \~. The
left side is a logical vector created using one or more vectors and
logical operators. The right side is the value to use when the left side
is TRUE. If no cases are TRUE (i.e., none of the arguments' left sides
are TRUE) then a NA is returned. The `TRUE ~ default_result` at the end
serves as a catch-all for any observation that does not meet a defined
condition:

::::: cell
:::: cell-output-display
<div>

<figure class="figure">

<p><img src="../slides/images/dplyr_case_when.png" class="img-fluid figure-img" width="1920"/></p>

</figure>

</div>
::::
:::::

Syntax:

::: {#cb8 .sourceCode}
``` {.sourceCode .r .code-with-copy}
case_when(
  condition1 ~ result1,
  condition2 ~ result2,
  condition3 ~ result3,
  TRUE ~ default_result
)tree <- tree %>% mutate(DBH_class = case_when( dbh_cm > 0 & dbh_cm <= 2.5 ~ "seedling", dbh_cm > 2.5 & dbh_cm <= 10 ~ "sapling", dbh_cm > 10 & dbh_cm <= 30 ~ "pole", dbh_cm > 30 ~ "sawlog" )) %>% filter(year == 2007)
```
:::

In forestry, DBH_cm can be used to classify a tree using the following
classification:

| low | high | class      |
|:----|:-----|:-----------|
| 0   | 2.5  | "seedling" |
| 2.5 | 10   | "sapling"  |
| 10  | 30   | "pole"     |
| 30  | \-   | "sawlog"   |

> **Question 16: Use `mutate` and `case_when` to add a new column to you
> data.frame that classifies each tree into the proper DBH_class. Once
> done, limit your dataset to the year 2007 and report the number of
> each class with count**
:::::::

``` r
tree <- tree %>%  
+ mutate(dbh_class = case_when(
+ dbh_cm > 0 & dbh_cm <= 2.5  ~ "seedling",
+ dbh_cm > 2.5 & dbh_cm <= 10 ~ "sapling",
+ dbh_cm > 10 & dbh_cm <= 30  ~ "pole",
+ dbh_cm > 30                 ~ "sawlog"))


Count_7 <- tree %>% 
+ filter(year == 2007) %>% 
+ count(dbh_class)
```

| dbh_class |    n |
|:----------|-----:|
| pole      |  473 |
| sapling   | 1817 |
| sawlog    |    1 |

There are 473 pole trees, 1817 sapling trees, and 1 sawlog tree.

::: {.section .level2}

## 8. Summarizing {.anchored anchor-id="summarizing"}

`summarize()` collapses a `data.frame` to a single row. We can use
`summarize()` to compute summary statistics for one or more columns in a
`data.frame`. The first argument in `summarize()` is the data.frame and
subsequent arguments define how rows should be collapsed.

> **Question 17: Compute the mean DBH (in cm) and standard deviation of
> DBH (in cm) for all trees in 2007. Explain the values you found and
> their statistical meaning.**

`summarize()` is often the most useful when applied to groups of data
(e.g species) rather then entire data sets!
:::

``` r
dbh_07_summarize <- tree %>%  
+ filter(year == 2007) %>%  
+ summarize(dbh_mean_07 = mean(dbh_cm), dbh_sd_07 = sd(dbh_cm))
```

| dbh_mean_07 | dbh_sd_07 |
|------------:|----------:|
|    8.046755 |  3.069321 |

The mean dbh is 8.047 cm in 2007, and the standard deviation is 3.069.
Mean is the average of a dataset, while standard deviation is a measure
of variance in a datset calculated by averaging a squared sum of
distances from the mean and taking its square root. A high standard
deviation suggests high variation in the data, since the sample size is
relatively high at 2291 observations for 2007.

:::::: {#grouped-data .section .level2}
## 9. Grouped data {.anchored anchor-id="grouped-data"}

`()` is used to group data by one or more variables. It is commonly used
in conjunction with functions like `summarize()`, `mutate()`, or
`filter()` to perform operations on subsets of data within a data.frame.

The first argument in `group_by()` is the d`ata.frame` to group and
subsequent arguments identify the columns, or combination of columns,
that define row membership to a group.

:::: cell
::: {#cb9 .sourceCode .cell-code}
``` {.sourceCode .r .code-with-copy}
trees_by_id <- group_by(trees, treeID)
glimpse(trees_by_id)

#> Rows: 131,386
#> Columns: 13
#> Groups: treeID [2,291]
#> $ treeID    <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
#> $ standID   <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
#> $ stand     <chr> "A1", "A1", "A1", "A1", "A1", "A1", "A1", "A1", "A1", "A1", "A1"…
#> $ year      <int> 1960, 1961, 1962, 1963, 1964, 1965, 1966, 1967, 1968, 1969, 1970…
#> ...
```
:::
::::

::: {#how-do-dplyr-functions-behave-given-a-grouped-data.frame .section .level3}
### How do `dplyr` functions behave given a grouped `data.frame`? {.anchored anchor-id="how-do-dplyr-functions-behave-given-a-grouped-data.frame"}

If `filter()` is passed a grouped data.frame and the filtering condition
uses a summary function or group characteristic (e.g., number of rows
computed using the n()), the result will be group specific.

Similarly, `slice()` and its various flavors subset rows within each
group.

Passing grouped and ungrouped data to `arrange()` gives the same result,
unless you set the function's optional argument `.by_group` to TRUE, in
which case it will order first by the grouping.

Recall, the functions select(), rename(), mutate(), transmute(), and
relocate() operate on data.frame columns. Because `rename()` only
affects the column name and position, its behavior is the same given
grouped or ungrouped data.

Similarly, a grouped select() is the same as an ungrouped select(),
except grouping columns are always included in the resulting column
subset. Similar to a grouped `filter()`, a grouped `mutate()` has
different behavior if your new column definition uses a summary function
or some other group specific characteristic (e.g. max/min/n()/lag/diff,
etc.).

As mentioned, `summarize()` is most useful when applied to grouped data.
Given a grouped`data.frame`, column summaries requested from
`summarize()` are applied to each group.

Each time you apply `summarize()` to a grouped `data.frame`, the default
behavior is to remove the last grouping level.

> **Question 18: Compute the *per species* mean tree age using only
> those ages recorded in 2003. Identify the three species with the
> oldest mean age.**
:::

year 2003

group by species

take the average age of each species with summarize

arrange -species_age

slice n = 3

| species | sp_age_avg |
|:--------|-----------:|
| THOC    |  126.63830 |
| FRNI    |   83.08333 |
| PIST    |   73.28571 |

The three oldest -growing species in 2003 are *Thuja occidentalis,
Fraxinus nigra*, and *Pinus strobus*.

## 10. Counting {.anchored anchor-id="counting"}

We often need to know the number of rows, perhaps by group, within a
dataset. Rows are counted using the `n()` helper function, which is a
*context dependent function* used within `dplyr` verb functions. It
takes no arguments and returns the context specific group size. We see
`n()` used most often in `summarize()` and `mutate()` to count rows in
groups.

The number of distinct values in a discrete variable is also often of
interest (e.g., number of distinct plot numbers or species).
`n_distinct()` returns the number of unique values in one or more
variable. Like `n()`, when applied to a grouped `data.frame` within a
verb function,`n_distinct()` returns the number of group specific
distinct values:

> **Question 19: In a single summarize call, find the number of unique
> years with records in the data set along with the first and last year
> recorded?**
::::::

> ``` r
> tree %>%
>
> + summarize( 
> + n_years = n_distinct(year), 
> + first_year = min(year, na.rm = TRUE), 
> + last_year = max(year, na.rm = TRUE) 
> )
> ```

| n_years | first_year | last_year |
|:--------|------------|----------:|
| 111     | 1897       |      2007 |

::: {.section .level2}
> **Question 20: Determine the stands with the largest number of unique
> years recorded. Report all stands with largest (or tied with the
> largest) temporal record.**
:::
:::::::::::::::::::::::::::::

``` r
tree %>% 
+     group_by(standID) %>% 
+     summarize(n_years = n_distinct(year)) %>% 
+     slice_max(n_years) %>% 
+ kable()
```

| standID | n_years |
|--------:|--------:|
|       1 |     111 |
|      15 |     111 |
|      16 |     111 |
|      17 |     111 |
|      24 |     111 |

Stands 1, 15, 16, 17, and 24 all have 111 years of records.

::: {#final-question .section .level1}
# Final Question:

We are interested in the annual DBH growth rate of each species through
time, but we only want to include trees with at least a 10-year growth
record. To identify this, we need to identify

the per year growth made by each tree,

their total growth record,

and then average that,

and compute the standard deviation, across the species.

```         
tree <- tree %>%  + mutate(dbh_lag = lag(dbh_cm, n=1))
```

So how by much did each tree grow each year?

Is there a difference between calculating total growth over total years
versus calculating growth each year, aggregating, and then dividing the
total growth per year?

> Use a combination of dplyr verbs to compute these values and report
> the 3 species with the fastest growth, and the 3 species with the
> slowest growth. (\*\* You will need to use either `lag()` or `diff()`
> in your compuation. You can learn more about each in the Help pages)

> Lastly, find and include an image of the fastest growing species. Add
> the image to your images directory.
:::

::: {#rubric .section .level1}
# Rubric

Created as an R project with a proper project structure (data, images,
docs) (5)

20 Questions \@ 3 points each (60). Answered with code and full
sentences.

Final Question (15)

Correct image with caption (5)

Connect your project to github and submit a URL of the rendered document
(10)

**Total**: 100
:::
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
