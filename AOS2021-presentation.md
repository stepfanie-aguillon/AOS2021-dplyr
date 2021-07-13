2021 AOS Presentation
================
Stepfanie M Aguillon
7/13/2021

## Load packages

To start, load all of the required packages.

``` r
library(tidyverse)
library(palmerpenguins)
data(package="palmerpenguins")
```

`dplyr` is a package within the `tidyverse`, but all of the packages are
really useful so we’ll load the entire `tidyverse`.

`palmerpenguins` contains an example dataset that we’ll be working with.
(This is to avoid the commonly used `iris` dataset, which was published
in the Annals of Eugenics\!) More details on the \`palmerpenguins’
package can be found here
<https://allisonhorst.github.io/palmerpenguins/>

## About the dataset

The `penguins` dataset contains data for 344 penguins from 3 different
species collected from 3 islands. There are 8 different variables for
each individual row. Let’s look at the first few
rows:

``` r
# throughout this document, the only purpose of the function `kable` is to provide nice visuals of the tables
kable(head(penguins))
```

| species | island    | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex    | year |
| :------ | :-------- | ---------------: | --------------: | ------------------: | ------------: | :----- | ---: |
| Adelie  | Torgersen |             39.1 |            18.7 |                 181 |          3750 | male   | 2007 |
| Adelie  | Torgersen |             39.5 |            17.4 |                 186 |          3800 | female | 2007 |
| Adelie  | Torgersen |             40.3 |            18.0 |                 195 |          3250 | female | 2007 |
| Adelie  | Torgersen |               NA |              NA |                  NA |            NA | NA     | 2007 |
| Adelie  | Torgersen |             36.7 |            19.3 |                 193 |          3450 | female | 2007 |
| Adelie  | Torgersen |             39.3 |            20.6 |                 190 |          3650 | male   | 2007 |

Penguin species = Adelie, Chinstrap, Gentoo

Island names = Biscoe, Dream, Torgersen

## `dplyr` is great for data processing

Now that we have a basic understanding of the setup of the dataset,
let’s look at some of the useful functions that `dplyr` offers\!

### 1\. Working with rows

There are a lot of things you might want to do with the **observations**
in your dataset. Maybe you want to separate observations out for a
particular species or island (`filter`; example 1.1)? Or maybe you’d
like to arrange your observations based on body mass (`arrange`; example
1.2)? Or maybe you’d like a random subset of your dataset (`sample_n`;
example 1.3)?

#### Example 1.1 (`filter`)

Make a dataset with ONLY Gentoo penguins

``` r
gentoo <- filter(penguins, species=="Gentoo")
kable(head(gentoo))
```

| species | island | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex    | year |
| :------ | :----- | ---------------: | --------------: | ------------------: | ------------: | :----- | ---: |
| Gentoo  | Biscoe |             46.1 |            13.2 |                 211 |          4500 | female | 2007 |
| Gentoo  | Biscoe |             50.0 |            16.3 |                 230 |          5700 | male   | 2007 |
| Gentoo  | Biscoe |             48.7 |            14.1 |                 210 |          4450 | female | 2007 |
| Gentoo  | Biscoe |             50.0 |            15.2 |                 218 |          5700 | male   | 2007 |
| Gentoo  | Biscoe |             47.6 |            14.5 |                 215 |          5400 | male   | 2007 |
| Gentoo  | Biscoe |             46.5 |            13.5 |                 210 |          4550 | female | 2007 |

Make a datset with ALL species, but only for Dream Island

``` r
dream <- filter(penguins, island=="Dream")
kable(head(dream))
```

| species | island | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex    | year |
| :------ | :----- | ---------------: | --------------: | ------------------: | ------------: | :----- | ---: |
| Adelie  | Dream  |             39.5 |            16.7 |                 178 |          3250 | female | 2007 |
| Adelie  | Dream  |             37.2 |            18.1 |                 178 |          3900 | male   | 2007 |
| Adelie  | Dream  |             39.5 |            17.8 |                 188 |          3300 | female | 2007 |
| Adelie  | Dream  |             40.9 |            18.9 |                 184 |          3900 | male   | 2007 |
| Adelie  | Dream  |             36.4 |            17.0 |                 195 |          3325 | female | 2007 |
| Adelie  | Dream  |             39.2 |            21.1 |                 196 |          4150 | male   | 2007 |

#### Example 1.2 (`arrange`)

Arrange our dataset based on body mass

``` r
body_mass <- arrange(penguins, body_mass_g)
kable(head(body_mass))
```

| species   | island    | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex    | year |
| :-------- | :-------- | ---------------: | --------------: | ------------------: | ------------: | :----- | ---: |
| Chinstrap | Dream     |             46.9 |            16.6 |                 192 |          2700 | female | 2008 |
| Adelie    | Biscoe    |             36.5 |            16.6 |                 181 |          2850 | female | 2008 |
| Adelie    | Biscoe    |             36.4 |            17.1 |                 184 |          2850 | female | 2008 |
| Adelie    | Biscoe    |             34.5 |            18.1 |                 187 |          2900 | female | 2008 |
| Adelie    | Dream     |             33.1 |            16.1 |                 178 |          2900 | female | 2008 |
| Adelie    | Torgersen |             38.6 |            17.0 |                 188 |          2900 | female | 2009 |

#### Example 1.3 (`sample_n`)

Take a random sample of 5 observations (without replacement) from the
dataset

``` r
random_sample <- sample_n(penguins, 5, replace=FALSE)
kable(head(random_sample))
```

| species | island    | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex    | year |
| :------ | :-------- | ---------------: | --------------: | ------------------: | ------------: | :----- | ---: |
| Adelie  | Torgersen |             36.7 |            18.8 |                 187 |          3800 | female | 2008 |
| Adelie  | Torgersen |             39.7 |            18.4 |                 190 |          3900 | male   | 2008 |
| Adelie  | Biscoe    |             35.9 |            19.2 |                 189 |          3800 | female | 2007 |
| Adelie  | Biscoe    |             37.9 |            18.6 |                 172 |          3150 | female | 2007 |
| Adelie  | Torgersen |             37.3 |            20.5 |                 199 |          3775 | male   | 2009 |

### 2\. Working with columns

We’ve worked through some useful functions for working directly with
your observations, but you might also want to work with your different
**variables**. Maybe you want to select only those variables that
describe the bill (`select`; example 2.1)? Or maybe you’d like to rename
a variable (`rename`; example 2.2)? Or maybe you’d like a whole NEW
variable (`mutate`; example 2.3)?

#### Example 2.1 (`select`)

Make a dataset with just the variables that describe the bill for each
species

``` r
bill_variables <- select(penguins, species, bill_length_mm, bill_depth_mm)
# syntax within select is the dataframe, and then all the columns you would like to keep separated by commas
kable(head(bill_variables))
```

| species | bill\_length\_mm | bill\_depth\_mm |
| :------ | ---------------: | --------------: |
| Adelie  |             39.1 |            18.7 |
| Adelie  |             39.5 |            17.4 |
| Adelie  |             40.3 |            18.0 |
| Adelie  |               NA |              NA |
| Adelie  |             36.7 |            19.3 |
| Adelie  |             39.3 |            20.6 |

#### Example 2.2 (`rename`)

Make a dataset that renames the `flipper_length_mm` column to something
easier to type

``` r
new_flipper <- rename(penguins, flipper = flipper_length_mm)
kable(head(new_flipper))
```

| species | island    | bill\_length\_mm | bill\_depth\_mm | flipper | body\_mass\_g | sex    | year |
| :------ | :-------- | ---------------: | --------------: | ------: | ------------: | :----- | ---: |
| Adelie  | Torgersen |             39.1 |            18.7 |     181 |          3750 | male   | 2007 |
| Adelie  | Torgersen |             39.5 |            17.4 |     186 |          3800 | female | 2007 |
| Adelie  | Torgersen |             40.3 |            18.0 |     195 |          3250 | female | 2007 |
| Adelie  | Torgersen |               NA |              NA |      NA |            NA | NA     | 2007 |
| Adelie  | Torgersen |             36.7 |            19.3 |     193 |          3450 | female | 2007 |
| Adelie  | Torgersen |             39.3 |            20.6 |     190 |          3650 | male   | 2007 |

#### Example 2.3 (`mutate`)

Create a new variable to describe bill size
(depth/length)

``` r
new_penguins <- mutate(bill_variables, overall_bill=bill_depth_mm/bill_length_mm)
# syntax here is new_variable = equation based on existing columns
kable(head(new_penguins))
```

| species | bill\_length\_mm | bill\_depth\_mm | overall\_bill |
| :------ | ---------------: | --------------: | ------------: |
| Adelie  |             39.1 |            18.7 |     0.4782609 |
| Adelie  |             39.5 |            17.4 |     0.4405063 |
| Adelie  |             40.3 |            18.0 |     0.4466501 |
| Adelie  |               NA |              NA |            NA |
| Adelie  |             36.7 |            19.3 |     0.5258856 |
| Adelie  |             39.3 |            20.6 |     0.5241730 |

### 3\. Summarizing your dataset

We’ve now learned some useful functions to work with both observations
(rows) and variables (columns) within your dataset. But you might also
want to do some summarizing of your entire dataset\! `dplyr` offers the
really useful function `summarize` (or `summarise`) to help with this\!
`summarize` is really useful when combined with `group_by` a function
that groups observations based on shared values of a variable. Maybe
you’d like to know the average flipper size and body mass for each
species within your dataset (example 3.1)? Or maybe you’d like to know
if the average body size has changed across years for each species
(example 3.2)?

#### Example 3.1 (`summarize`)

Summarize the average flipper size and body mass for each species.

``` r
summarize1 <- group_by(penguins, species) %>%
  summarize(avg_flipper = mean(na.omit(flipper_length_mm)), avg_body_mass = mean(na.omit(body_mass_g)))
kable(head(summarize1))
```

| species   | avg\_flipper | avg\_body\_mass |
| :-------- | -----------: | --------------: |
| Adelie    |     189.9536 |        3700.662 |
| Chinstrap |     195.8235 |        3733.088 |
| Gentoo    |     217.1870 |        5076.016 |

``` r
# na.omit() removes NAs from the calculation
# See the final section for more details on the %>% notation
```

#### Example 3.2 (`summarize`)

Summarize the average body size within each species for each year

``` r
summarize2 <- group_by(penguins, species, year) %>%
  summarize(avg_body_mass = mean(na.omit(body_mass_g)))
kable(head(summarize2))
```

| species   | year | avg\_body\_mass |
| :-------- | ---: | --------------: |
| Adelie    | 2007 |        3696.429 |
| Adelie    | 2008 |        3742.000 |
| Adelie    | 2009 |        3664.904 |
| Chinstrap | 2007 |        3694.231 |
| Chinstrap | 2008 |        3800.000 |
| Chinstrap | 2009 |        3725.000 |

``` r
# na.omit() removes NAs from the calculation
# See the final section for more details on the %>% notation
```

### 4\. Joining multiple datasets

You may want to combine **multiple** datasets together\! This is really
useful when you have information spread across multiple datafiles. There
are a number of join functions within `dplyr`, including `left_join`,
`right_join`, `inner_join`, and `full_join`. Depending on your goal,
different join functions may be more or less appropriate. Maybe you have
additional information for each individual in a separate datafile that
you’d like to work with (exercise 4.1)?

Here is a second dataset that we can join to the one we’ve been working
with. This is a subset of columns from the raw dataframe
(`penguins_raw`) that is also available through
`palmerpenguins`.

``` r
#subsetting the larger raw penguins dataframe to use as an example second dataframe to join with
small_penguins_raw <- select(penguins_raw, `Island`, `Culmen Length (mm)`, `Culmen Depth (mm)`, `Flipper Length (mm)`, `Stage`, `Clutch Completion`) %>%
#rename variables to match the dataframe we've been working with
  rename(island=Island, bill_length_mm = `Culmen Length (mm)`, bill_depth_mm = `Culmen Depth (mm)`, flipper_length_mm = `Flipper Length (mm)`, stage = Stage, clutch_complete = `Clutch Completion`)

#in most cases, you would have a "key" column that is identical between your two dataframes, here I'm going to use a combination of Island ID, bill length, bill depth, and flipper length to identify individuals and join the two dataframes
```

#### Example 4.1

We now have another dataframe with information on the stage when
observations were taken and if the individual completed their clutch.
We’ll join using `inner_join` to keep only those rows that are in both
dataframes.

``` r
joined_df <- inner_join(penguins, small_penguins_raw, by=c("island","bill_length_mm","bill_depth_mm","flipper_length_mm"))
#Now we have two additional columns (stage and clutch_complete) that provide more information on each individual in the dataset!
kable(head(joined_df))
```

| species | island    | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex    | year | stage              | clutch\_complete |
| :------ | :-------- | ---------------: | --------------: | ------------------: | ------------: | :----- | ---: | :----------------- | :--------------- |
| Adelie  | Torgersen |             39.1 |            18.7 |                 181 |          3750 | male   | 2007 | Adult, 1 Egg Stage | Yes              |
| Adelie  | Torgersen |             39.5 |            17.4 |                 186 |          3800 | female | 2007 | Adult, 1 Egg Stage | Yes              |
| Adelie  | Torgersen |             40.3 |            18.0 |                 195 |          3250 | female | 2007 | Adult, 1 Egg Stage | Yes              |
| Adelie  | Torgersen |               NA |              NA |                  NA |            NA | NA     | 2007 | Adult, 1 Egg Stage | Yes              |
| Adelie  | Torgersen |             36.7 |            19.3 |                 193 |          3450 | female | 2007 | Adult, 1 Egg Stage | Yes              |
| Adelie  | Torgersen |             39.3 |            20.6 |                 190 |          3650 | male   | 2007 | Adult, 1 Egg Stage | Yes              |

### 5\. Combining it all together

Finally, you may want to combine multiple approaches without defining a
new dataframe at each step\! The `%>%` (pipe operator) is really handy
for this kind of approach\! It allows you to string together multiple
functions within `dplyr` (and the `tidyverse` more generally), and helps
make your code more streamlined.

#### Example 5.1

Maybe you’re only interested in bill measurements of Chinstrap penguins
and would like to make a new variable that describes bill size and then
summarize across sexes. That sounds like a lot of work\! But it can
actually be accomplished with just a few lines of
code\!

``` r
# when using this notation, you no longer need to indicate the dataframe WITHIN each function because you tell dplyr the dataframe you're working with at the very beginning (by writing: penguins %>%)

# start by telling dplyr the dataframe you're working with 
penguins %>%
  # use filter to select your species (section 1)
  filter(species=="Chinstrap") %>%
  # use select to choose the variables you're interested in (section 2)
  select(species, sex, bill_length_mm, bill_depth_mm) %>%
  # use mutate to create your new variable (section 2)
  mutate(overall_bill=bill_depth_mm/bill_length_mm) %>%
  # use group_by and summarize to create your summary (section 3)
  group_by(sex) %>%
  summarize(avg_bill_length=mean(na.omit(bill_length_mm)), avg_bill_depth=mean(na.omit(bill_depth_mm)), avg_overall_bill=mean(na.omit(overall_bill))) %>%
  kable()
```

| sex    | avg\_bill\_length | avg\_bill\_depth | avg\_overall\_bill |
| :----- | ----------------: | ---------------: | -----------------: |
| female |          46.57353 |         17.58824 |          0.3788913 |
| male   |          51.09412 |         19.25294 |          0.3769551 |
