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