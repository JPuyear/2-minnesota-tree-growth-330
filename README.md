# Lab 2: minnesota-tree-growth
RStudio

| treeID| standID| year| rad_ib|
|------:|-------:|----:|------:|
|     50|       3| 2007| 47.396|
|     56|       3| 2007| 48.440|
|     36|       3| 2007| 54.925|



| treeID| standID| age|
|------:|-------:|---:|
|     24|       2| 263|
|     25|       2| 259|
|   1595|      24| 212|
|   1598|      24| 206|
|   1712|      26| 206|


Question 3
'''r
> abies_pinus <- tree %>% 
+ filter(species %in% c("ABBA", "PIST"))
> nrow(abies_pinus)
[1] 17221

> smallest3_07 <- tree %>% 
+ select(treeID, standID, year, rad_ib) %>% 
+ filter(year == 2007, standID == 3) %>% 
+ slice_min(order_by = rad_ib, n = 3)


Question 8

| treeID|   rad_ib| age|
|------:|--------:|---:|
|    128| 238.8850|  82|
|    157| 217.8700|  85|
|    135| 210.1874|  84|


Question 15

|tree_old |      n|
|:--------|------:|
|FALSE    |   6951|
|TRUE     | 124435|



|dbh_class |      n|
|:---------|------:|
|pole      |  12692|
|sapling   | 100348|
|sawlog    |     17|
|seedling  |  18329|

|dbh_class |    n|
|:---------|----:|
|pole      |  473|
|sapling   | 1817|
|sawlog    |    1|

| dbh_mean_07| dbh_sd_07|
|-----------:|---------:|
|    8.046755|  3.069321|



|species | sp_age_avg|
|:-------|----------:|
|THOC    |  126.63830|
|FRNI    |   83.08333|
|PIST    |   73.28571|

> tree %>% 
+     summarize(
+         n_years = n_distinct(year), 
+         first_year = min(year, na.rm = TRUE), 
+         last_year = max(year, na.rm = TRUE)
+     )
  n_years first_year last_year
1     111       1897      2007

tree %>%

+ summarize( 

+ n_years = n_distinct(year), 

+ first_year = min(year, na.rm = TRUE), 

+ last_year = max(year, na.rm = TRUE) 

+ ) n_years first_year last_year 1 111 1897 2007

  | n_years  |first_year | last_year|
  |:---------|-----------|---------:|
1 |    111   |    1897   |    2007  |

| standID| n_years|
|-------:|-------:|
|       1|     111|
|      15|     111|
|      16|     111|
|      17|     111|
|      24|     111|

> tree %>% 
+     group_by(standID) %>% 
+     summarize(n_years = n_distinct(year)) %>% 
+     slice_max(n_years) %>% 
+ kable()
