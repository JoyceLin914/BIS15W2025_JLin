---
title: "Homework 5"
author: "Joyce"
date: "2025-01-26"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---
need to look at the readme file to answer the questions
## Instructions
Answer the following questions and/or complete the exercises in RMarkdown. Please embed all of your code and push the final work to your repository. Your report should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run.  

## Load the tidyverse

```r
library("tidyverse")
library("janitor")
```

## Data 
For this assignment, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the data folder.   

**1. Load `IvindoData_DryadVersion.csv` and store it as a new object called `gabon`.**

```r
gabon <- read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**2. Use one or more of the summary functions you have learned to get an idea of the structure of the data.**  

```r
summary(gabon)
```

```
##    TransectID       Distance        HuntCat          NumHouseholds  
##  Min.   : 1.00   Min.   : 2.700   Length:24          Min.   :13.00  
##  1st Qu.: 5.75   1st Qu.: 5.668   Class :character   1st Qu.:24.75  
##  Median :14.50   Median : 9.720   Mode  :character   Median :29.00  
##  Mean   :13.50   Mean   :11.879                      Mean   :37.88  
##  3rd Qu.:20.25   3rd Qu.:17.683                      3rd Qu.:54.00  
##  Max.   :27.00   Max.   :26.760                      Max.   :73.00  
##    LandUse             Veg_Rich       Veg_Stems       Veg_liana     
##  Length:24          Min.   :10.88   Min.   :23.44   Min.   : 4.750  
##  Class :character   1st Qu.:13.10   1st Qu.:28.69   1st Qu.: 9.033  
##  Mode  :character   Median :14.94   Median :32.45   Median :11.940  
##                     Mean   :14.83   Mean   :32.80   Mean   :11.040  
##                     3rd Qu.:16.54   3rd Qu.:37.08   3rd Qu.:13.250  
##                     Max.   :18.75   Max.   :47.56   Max.   :16.380  
##     Veg_DBH        Veg_Canopy    Veg_Understory     RA_Apes      
##  Min.   :28.45   Min.   :2.500   Min.   :2.380   Min.   : 0.000  
##  1st Qu.:40.65   1st Qu.:3.250   1st Qu.:2.875   1st Qu.: 0.000  
##  Median :43.90   Median :3.430   Median :3.000   Median : 0.485  
##  Mean   :46.09   Mean   :3.469   Mean   :3.020   Mean   : 2.045  
##  3rd Qu.:50.58   3rd Qu.:3.750   3rd Qu.:3.167   3rd Qu.: 3.815  
##  Max.   :76.48   Max.   :4.000   Max.   :3.880   Max.   :12.930  
##     RA_Birds      RA_Elephant       RA_Monkeys      RA_Rodent    
##  Min.   :31.56   Min.   :0.0000   Min.   : 5.84   Min.   :1.060  
##  1st Qu.:52.51   1st Qu.:0.0000   1st Qu.:22.70   1st Qu.:2.047  
##  Median :57.90   Median :0.3600   Median :31.74   Median :3.230  
##  Mean   :58.64   Mean   :0.5450   Mean   :31.30   Mean   :3.278  
##  3rd Qu.:68.17   3rd Qu.:0.8925   3rd Qu.:39.88   3rd Qu.:4.093  
##  Max.   :85.03   Max.   :2.3000   Max.   :54.12   Max.   :6.310  
##   RA_Ungulate     Rich_AllSpecies Evenness_AllSpecies Diversity_AllSpecies
##  Min.   : 0.000   Min.   :15.00   Min.   :0.6680      Min.   :1.966       
##  1st Qu.: 1.232   1st Qu.:19.00   1st Qu.:0.7542      1st Qu.:2.248       
##  Median : 2.545   Median :20.00   Median :0.7760      Median :2.316       
##  Mean   : 4.166   Mean   :20.21   Mean   :0.7699      Mean   :2.310       
##  3rd Qu.: 5.157   3rd Qu.:22.00   3rd Qu.:0.8083      3rd Qu.:2.429       
##  Max.   :13.860   Max.   :24.00   Max.   :0.8330      Max.   :2.566       
##  Rich_BirdSpecies Evenness_BirdSpecies Diversity_BirdSpecies Rich_MammalSpecies
##  Min.   : 8.00    Min.   :0.5590       Min.   :1.162         Min.   : 6.000    
##  1st Qu.:10.00    1st Qu.:0.6825       1st Qu.:1.603         1st Qu.: 9.000    
##  Median :11.00    Median :0.7220       Median :1.680         Median :10.000    
##  Mean   :10.33    Mean   :0.7137       Mean   :1.661         Mean   : 9.875    
##  3rd Qu.:11.00    3rd Qu.:0.7722       3rd Qu.:1.784         3rd Qu.:11.000    
##  Max.   :13.00    Max.   :0.8240       Max.   :2.008         Max.   :12.000    
##  Evenness_MammalSpecies Diversity_MammalSpecies
##  Min.   :0.6190         Min.   :1.378          
##  1st Qu.:0.7073         1st Qu.:1.567          
##  Median :0.7390         Median :1.699          
##  Mean   :0.7477         Mean   :1.698          
##  3rd Qu.:0.7847         3rd Qu.:1.815          
##  Max.   :0.8610         Max.   :2.065
```


```r
glimpse(gabon)
```

```
## Rows: 24
## Columns: 26
## $ TransectID              <dbl> 1, 2, 2, 3, 4, 5, 6, 7, 8, 9, 13, 14, 15, 16, …
## $ Distance                <dbl> 7.14, 17.31, 18.32, 20.85, 15.95, 17.47, 24.06…
## $ HuntCat                 <chr> "Moderate", "None", "None", "None", "None", "N…
## $ NumHouseholds           <dbl> 54, 54, 29, 29, 29, 29, 29, 54, 25, 73, 46, 56…
## $ LandUse                 <chr> "Park", "Park", "Park", "Logging", "Park", "Pa…
## $ Veg_Rich                <dbl> 16.67, 15.75, 16.88, 12.44, 17.13, 16.50, 14.7…
## $ Veg_Stems               <dbl> 31.20, 37.44, 32.33, 29.39, 36.00, 29.22, 31.2…
## $ Veg_liana               <dbl> 5.78, 13.25, 4.75, 9.78, 13.25, 12.88, 8.38, 8…
## $ Veg_DBH                 <dbl> 49.57, 34.59, 42.82, 36.62, 41.52, 44.07, 51.2…
## $ Veg_Canopy              <dbl> 3.78, 3.75, 3.43, 3.75, 3.88, 2.50, 4.00, 4.00…
## $ Veg_Understory          <dbl> 2.89, 3.88, 3.00, 2.75, 3.25, 3.00, 2.38, 2.71…
## $ RA_Apes                 <dbl> 1.87, 0.00, 4.49, 12.93, 0.00, 2.48, 3.78, 6.1…
## $ RA_Birds                <dbl> 52.66, 52.17, 37.44, 59.29, 52.62, 38.64, 42.6…
## $ RA_Elephant             <dbl> 0.00, 0.86, 1.33, 0.56, 1.00, 0.00, 1.11, 0.43…
## $ RA_Monkeys              <dbl> 38.59, 28.53, 41.82, 19.85, 41.34, 43.29, 46.2…
## $ RA_Rodent               <dbl> 4.22, 6.04, 1.06, 3.66, 2.52, 1.83, 3.10, 1.26…
## $ RA_Ungulate             <dbl> 2.66, 12.41, 13.86, 3.71, 2.53, 13.75, 3.10, 8…
## $ Rich_AllSpecies         <dbl> 22, 20, 22, 19, 20, 22, 23, 19, 19, 19, 21, 22…
## $ Evenness_AllSpecies     <dbl> 0.793, 0.773, 0.740, 0.681, 0.811, 0.786, 0.81…
## $ Diversity_AllSpecies    <dbl> 2.452, 2.314, 2.288, 2.006, 2.431, 2.429, 2.56…
## $ Rich_BirdSpecies        <dbl> 11, 10, 11, 8, 8, 10, 11, 11, 11, 9, 11, 11, 1…
## $ Evenness_BirdSpecies    <dbl> 0.732, 0.704, 0.688, 0.559, 0.799, 0.771, 0.80…
## $ Diversity_BirdSpecies   <dbl> 1.756, 1.620, 1.649, 1.162, 1.660, 1.775, 1.92…
## $ Rich_MammalSpecies      <dbl> 11, 10, 11, 11, 12, 12, 12, 8, 8, 10, 10, 11, …
## $ Evenness_MammalSpecies  <dbl> 0.736, 0.705, 0.650, 0.619, 0.736, 0.694, 0.77…
## $ Diversity_MammalSpecies <dbl> 1.764, 1.624, 1.558, 1.484, 1.829, 1.725, 1.92…
```
  
**3. Use `mutate()` Change the variables `HuntCat`, `LandUse`, and `TransectID` to factors.**

```r
gabon <- gabon %>% 
  mutate(HuntCat = as.factor(HuntCat)) %>% 
  mutate(LandUse = as.factor(LandUse)) %>% 
  mutate(TransectID = as.factor(TransectID))

is.factor(gabon$HuntCat)
```

```
## [1] TRUE
```

```r
is.factor(gabon$LandUse)
```

```
## [1] TRUE
```

```r
is.factor(gabon$TransectID)
```

```
## [1] TRUE
```

**4. Use `filter` to make three new dataframes focused only on 1. national parks, 2. logging concessions, and 3. neither. Have a look at the README in the data folder so you understand the variables.**

```r
gabon_2 <- filter(gabon, LandUse == "Park")
gabon_3 <- filter(gabon, LandUse == "Logging")
gabon_4 <- filter(gabon, LandUse == "Neither")
```

**5. How many transects are recorded for each land use type?**

```r
gabon_5 <- filter(gabon, LandUse %in% c("Park","Logging", "Neither"))
table(gabon_5$LandUse)
```

```
## 
## Logging Neither    Park 
##      13       4       7
```

National parks has 7 transect ID, Logging has 13 transect ID, and neither has 4 transect ID.

**6. For which land use type (national parks, logging, or neither) is average all species diversity the greatest?**

```r
mean(gabon_2$Diversity_AllSpecies)
```

```
## [1] 2.425143
```


```r
mean(gabon_3$Diversity_AllSpecies)
```

```
## [1] 2.232538
```


```r
mean(gabon_4$Diversity_AllSpecies)
```

```
## [1] 2.3575
```
National Parks has the highest average all species diversity.

**7. Use `filter` to find the transect that has the highest relative abundance of elephants. What land use type is this? Use `arrange()` to sort your results.** 

```r
gabon %>% 
  select(TransectID, RA_Elephant, LandUse) %>% 
  arrange(-RA_Elephant)
```

```
## # A tibble: 24 × 3
##    TransectID RA_Elephant LandUse
##    <fct>            <dbl> <fct>  
##  1 18                2.3  Logging
##  2 8                 2.2  Neither
##  3 2                 1.33 Park   
##  4 6                 1.11 Park   
##  5 4                 1    Park   
##  6 13                0.99 Logging
##  7 2                 0.86 Park   
##  8 21                0.77 Neither
##  9 3                 0.56 Logging
## 10 14                0.52 Logging
## # ℹ 14 more rows
```
Transect 18 has the highest relative abundance of 2.30, and the type of land use is Logging.

**8. Use `filter` to find all transects that have greater than 15 tree species or a breast height diameter between 50 and 60cm.  **

```r
gabon %>% 
  select(TransectID, Veg_Rich, Veg_DBH) %>% 
  filter(Veg_Rich>15 | between(Veg_DBH, 50, 60)) 
```

```
## # A tibble: 14 × 3
##    TransectID Veg_Rich Veg_DBH
##    <fct>         <dbl>   <dbl>
##  1 1              16.7    49.6
##  2 2              15.8    34.6
##  3 2              16.9    42.8
##  4 4              17.1    41.5
##  5 5              16.5    44.1
##  6 6              14.8    51.2
##  7 9              16      69.3
##  8 14             15.8    52.1
##  9 15             10.9    54.8
## 10 17             14.2    57.7
## 11 21             16.2    50.4
## 12 22             17.1    39.3
## 13 24             16.8    44.2
## 14 26             18.8    35.6
```

**9.Which transects and land use types have more than 10 tree species and 10 mammal species? Use `arrange()` to sort by the number of tree species.**

```r
gabon %>% 
  select(TransectID, LandUse, Veg_Rich, Rich_MammalSpecies) %>% 
  filter(Veg_Rich > 10 & Rich_MammalSpecies > 10) %>% 
  arrange(-Veg_Rich)
```

```
## # A tibble: 9 × 4
##   TransectID LandUse Veg_Rich Rich_MammalSpecies
##   <fct>      <fct>      <dbl>              <dbl>
## 1 4          Park        17.1                 12
## 2 22         Logging     17.1                 12
## 3 2          Park        16.9                 11
## 4 24         Park        16.8                 12
## 5 1          Park        16.7                 11
## 6 5          Park        16.5                 12
## 7 14         Logging     15.8                 11
## 8 6          Park        14.8                 12
## 9 3          Logging     12.4                 11
```

**10. Explore the data! Develop one question on your own that includes at least two lines of code. **
Which transects and land use types have the most number of households in the nearest village to each transect and have a high hunting intensity?
Sort the data by the number of households.

```r
gabon %>% 
  select(TransectID, LandUse, NumHouseholds, HuntCat) %>% 
  filter(HuntCat == "High") %>% 
  arrange(-NumHouseholds)
```

```
## # A tibble: 7 × 4
##   TransectID LandUse NumHouseholds HuntCat
##   <fct>      <fct>           <dbl> <fct>  
## 1 9          Logging            73 High   
## 2 15         Neither            46 High   
## 3 8          Neither            25 High   
## 4 21         Neither            24 High   
## 5 17         Neither            19 High   
## 6 22         Logging            13 High   
## 7 27         Logging            13 High
```
Transect ID 9 with a logging land use has the highest number of households, which is 73.

## Knit and Upload
Please knit your work as a .pdf or .html file and upload to Canvas. Homework is due before the start of the next lab. No late work is accepted. Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  
