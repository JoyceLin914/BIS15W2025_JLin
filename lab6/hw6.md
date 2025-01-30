---
title: "Homework 6"
author: "Joyce"
date: "2025-01-29"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and/or complete the exercises in RMarkdown. Please embed all of your code and push the final work to your repository. Your report should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run.  

## Load the tidyverse

```r
library("tidyverse")
library("janitor")
```

## Load the superhero data
Let's have a little fun with this one! We are going to explore data on superheroes. These are data taken from comic books and assembled by devoted fans. The include a good mix of categorical and continuous data.  Data taken from: https://www.kaggle.com/claudiodavi/superhero-set  

Load the `heroes_information.csv` and `super_hero_powers.csv` data. Make sure the columns are cleanly named.

```r
superhero_info <- read_csv("data/heroes_information.csv", na = c("", "-99", "-")) %>% clean_names()
```

```
## Rows: 734 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (8): name, Gender, Eye color, Race, Hair color, Publisher, Skin color, A...
## dbl (2): Height, Weight
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
superhero_powers <- read_csv("data/super_hero_powers.csv", na = c("", "-99", "-")) %>% clean_names()
```

```
## Rows: 667 Columns: 168
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr   (1): hero_names
## lgl (167): Agility, Accelerated Healing, Lantern Power Ring, Dimensional Awa...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. For the superhero_info data, how many bad, good, and neutral superheros are there? Try using count() and/ or tabyl().

```r
superhero_info %>% 
  count(alignment)
```

```
## # A tibble: 4 × 2
##   alignment     n
##   <chr>     <int>
## 1 bad         207
## 2 good        496
## 3 neutral      24
## 4 <NA>          7
```


```r
superhero_info %>% 
  tabyl(alignment)
```

```
##  alignment   n     percent valid_percent
##        bad 207 0.282016349    0.28473177
##       good 496 0.675749319    0.68225585
##    neutral  24 0.032697548    0.03301238
##       <NA>   7 0.009536785            NA
```

2. Notice that we have some bad superheros! Who are they? List their names below.  

```r
superhero_info %>% 
  select(name, alignment) %>% 
  filter(alignment=="bad") 
```

```
## # A tibble: 207 × 2
##    name          alignment
##    <chr>         <chr>    
##  1 Abomination   bad      
##  2 Abraxas       bad      
##  3 Absorbing Man bad      
##  4 Air-Walker    bad      
##  5 Ajax          bad      
##  6 Alex Mercer   bad      
##  7 Alien         bad      
##  8 Amazo         bad      
##  9 Ammo          bad      
## 10 Angela        bad      
## # ℹ 197 more rows
```


```r
superhero_info %>% 
  filter(alignment=="bad") %>% 
  select(name)
```

```
## # A tibble: 207 × 1
##    name         
##    <chr>        
##  1 Abomination  
##  2 Abraxas      
##  3 Absorbing Man
##  4 Air-Walker   
##  5 Ajax         
##  6 Alex Mercer  
##  7 Alien        
##  8 Amazo        
##  9 Ammo         
## 10 Angela       
## # ℹ 197 more rows
```

3. How many distinct "races" are represented in `superhero_info`?

```r
superhero_info %>% 
  summarize(n_races=n_distinct(race))
```

```
## # A tibble: 1 × 1
##   n_races
##     <int>
## 1      62
```

## Good and Bad
4. Let's make two different data frames, one focused on the "good guys" and another focused on the "bad guys".

```r
good_superhero <- superhero_info %>% 
  filter(alignment=="good")

good_superhero
```

```
## # A tibble: 496 × 10
##    name  gender eye_color race  hair_color height publisher skin_color alignment
##    <chr> <chr>  <chr>     <chr> <chr>       <dbl> <chr>     <chr>      <chr>    
##  1 A-Bo… Male   yellow    Human No Hair       203 Marvel C… <NA>       good     
##  2 Abe … Male   blue      Icth… No Hair       191 Dark Hor… blue       good     
##  3 Abin… Male   blue      Unga… No Hair       185 DC Comics red        good     
##  4 Adam… Male   blue      <NA>  Blond          NA NBC - He… <NA>       good     
##  5 Adam… Male   blue      Human Blond         185 DC Comics <NA>       good     
##  6 Agen… Female blue      <NA>  Blond         173 Marvel C… <NA>       good     
##  7 Agen… Male   brown     Human Brown         178 Marvel C… <NA>       good     
##  8 Agen… Male   <NA>      <NA>  <NA>          191 Marvel C… <NA>       good     
##  9 Alan… Male   blue      <NA>  Blond         180 DC Comics <NA>       good     
## 10 Alex… Male   <NA>      <NA>  <NA>           NA NBC - He… <NA>       good     
## # ℹ 486 more rows
## # ℹ 1 more variable: weight <dbl>
```


```r
bad_superhero <- superhero_info %>% 
  filter(alignment=="bad")
bad_superhero
```

```
## # A tibble: 207 × 10
##    name  gender eye_color race  hair_color height publisher skin_color alignment
##    <chr> <chr>  <chr>     <chr> <chr>       <dbl> <chr>     <chr>      <chr>    
##  1 Abom… Male   green     Huma… No Hair       203 Marvel C… <NA>       bad      
##  2 Abra… Male   blue      Cosm… Black          NA Marvel C… <NA>       bad      
##  3 Abso… Male   blue      Human No Hair       193 Marvel C… <NA>       bad      
##  4 Air-… Male   blue      <NA>  White         188 Marvel C… <NA>       bad      
##  5 Ajax  Male   brown     Cybo… Black         193 Marvel C… <NA>       bad      
##  6 Alex… Male   <NA>      Human <NA>           NA Wildstorm <NA>       bad      
##  7 Alien Male   <NA>      Xeno… No Hair       244 Dark Hor… black      bad      
##  8 Amazo Male   red       Andr… <NA>          257 DC Comics <NA>       bad      
##  9 Ammo  Male   brown     Human Black         188 Marvel C… <NA>       bad      
## 10 Ange… Female <NA>      <NA>  <NA>           NA Image Co… <NA>       bad      
## # ℹ 197 more rows
## # ℹ 1 more variable: weight <dbl>
```

5. Who are the good Vampires?

```r
superhero_info %>% 
  filter(alignment == "good" & race == "Vampire")
```

```
## # A tibble: 2 × 10
##   name  gender eye_color race   hair_color height publisher skin_color alignment
##   <chr> <chr>  <chr>     <chr>  <chr>       <dbl> <chr>     <chr>      <chr>    
## 1 Angel Male   <NA>      Vampi… <NA>           NA Dark Hor… <NA>       good     
## 2 Blade Male   brown     Vampi… Black         188 Marvel C… <NA>       good     
## # ℹ 1 more variable: weight <dbl>
```

6. Who has the height advantage- bad guys or good guys? Convert their height to meters and sort from tallest to shortest.  

```r
superhero_info %>% 
  mutate(height=height/100) %>% 
  filter(alignment == "good") %>% 
  arrange(-height)
```

```
## # A tibble: 496 × 10
##    name  gender eye_color race  hair_color height publisher skin_color alignment
##    <chr> <chr>  <chr>     <chr> <chr>       <dbl> <chr>     <chr>      <chr>    
##  1 Fin … Male   red       Kaka… No Hair      9.75 Marvel C… green      good     
##  2 Groot Male   yellow    Flor… <NA>         7.01 Marvel C… <NA>       good     
##  3 Wolf… Female green     <NA>  Auburn       3.66 Marvel C… <NA>       good     
##  4 Sasq… Male   red       <NA>  Orange       3.05 Marvel C… <NA>       good     
##  5 Ymir  Male   white     Fros… No Hair      3.05 Marvel C… white      good     
##  6 Rey   Female hazel     Human Brown        2.97 George L… <NA>       good     
##  7 Hell… Male   gold      Demon Black        2.59 Dark Hor… <NA>       good     
##  8 Hulk  Male   green     Huma… Green        2.44 Marvel C… green      good     
##  9 Kilo… Male   red       Bolo… No Hair      2.34 DC Comics pink       good     
## 10 Cloak Male   brown     <NA>  black        2.26 Marvel C… <NA>       good     
## # ℹ 486 more rows
## # ℹ 1 more variable: weight <dbl>
```


```r
superhero_info %>% 
  mutate(height=height/10) %>% 
  filter(alignment=="bad") %>% 
  arrange(-height)
```

```
## # A tibble: 207 × 10
##    name  gender eye_color race  hair_color height publisher skin_color alignment
##    <chr> <chr>  <chr>     <chr> <chr>       <dbl> <chr>     <chr>      <chr>    
##  1 MODOK Male   white     Cybo… Brownn       36.6 Marvel C… <NA>       bad      
##  2 Onsl… Male   red       Muta… No Hair      30.5 Marvel C… <NA>       bad      
##  3 Saur… Male   <NA>      Maiar <NA>         27.9 J. R. R.… <NA>       bad      
##  4 Solo… Male   black     Zomb… White        27.9 DC Comics <NA>       bad      
##  5 Dark… Male   red       New … No Hair      26.7 DC Comics grey       bad      
##  6 Amazo Male   red       Andr… <NA>         25.7 DC Comics <NA>       bad      
##  7 Alien Male   <NA>      Xeno… No Hair      24.4 Dark Hor… black      bad      
##  8 Doom… Male   red       Alien White        24.4 DC Comics <NA>       bad      
##  9 Kill… Male   red       Meta… No Hair      24.4 DC Comics green      bad      
## 10 Veno… Male   brown     Symb… Brown        22.9 Marvel C… <NA>       bad      
## # ℹ 197 more rows
## # ℹ 1 more variable: weight <dbl>
```

## `superhero_powers`
Have a quick look at the `superhero_powers` data frame.  

7. How many superheros have a combination of agility, stealth, super_strength, and stamina?

```r
clean_names(superhero_powers)
```

```
## # A tibble: 667 × 168
##    hero_names    agility accelerated_healing lantern_power_ring
##    <chr>         <lgl>   <lgl>               <lgl>             
##  1 3-D Man       TRUE    FALSE               FALSE             
##  2 A-Bomb        FALSE   TRUE                FALSE             
##  3 Abe Sapien    TRUE    TRUE                FALSE             
##  4 Abin Sur      FALSE   FALSE               TRUE              
##  5 Abomination   FALSE   TRUE                FALSE             
##  6 Abraxas       FALSE   FALSE               FALSE             
##  7 Absorbing Man FALSE   FALSE               FALSE             
##  8 Adam Monroe   FALSE   TRUE                FALSE             
##  9 Adam Strange  FALSE   FALSE               FALSE             
## 10 Agent Bob     FALSE   FALSE               FALSE             
## # ℹ 657 more rows
## # ℹ 164 more variables: dimensional_awareness <lgl>, cold_resistance <lgl>,
## #   durability <lgl>, stealth <lgl>, energy_absorption <lgl>, flight <lgl>,
## #   danger_sense <lgl>, underwater_breathing <lgl>, marksmanship <lgl>,
## #   weapons_master <lgl>, power_augmentation <lgl>, animal_attributes <lgl>,
## #   longevity <lgl>, intelligence <lgl>, super_strength <lgl>,
## #   cryokinesis <lgl>, telepathy <lgl>, energy_armor <lgl>, …
```


```r
superhero_powers %>% 
  filter(agility == "TRUE" & stealth== "TRUE" & super_strength=="TRUE" & stamina=="TRUE") %>% 
  summarize(n_names=n_distinct(hero_names))
```

```
## # A tibble: 1 × 1
##   n_names
##     <int>
## 1      40
```

8. Who is the most powerful superhero? Have a look at the code chunk below. Use the internet to annotate each line of code so you know how it works. It's OK to use AI to help you with this task.

```r
superhero_powers %>% # calls the superhero_powers df
  mutate(across(-1, ~ ifelse(. == TRUE, 1, 0))) %>% 
  # across the entire data frame, apply the following condition to every cell in all columns except the first column: if the data in the cell is "TRUE", convert it into "1", if the data is not "TRUE", convert it into "0"
  mutate(total_powers = rowSums(across(-1))) %>% 
  # add the sum of numbers for each row (except the first column) and name the new column "total_powers"
  select(hero_names, total_powers) %>%
  # only show data of the 2 columns "hero_names" and "total_powers"
  arrange(-total_powers)
```

```
## # A tibble: 667 × 2
##    hero_names        total_powers
##    <chr>                    <dbl>
##  1 Spectre                     49
##  2 Amazo                       44
##  3 Living Tribunal             35
##  4 Martian Manhunter           35
##  5 Man of Miracles             34
##  6 Captain Marvel              33
##  7 T-X                         33
##  8 Galactus                    32
##  9 T-1000                      32
## 10 Mister Mxyzptlk             31
## # ℹ 657 more rows
```

```r
  # sort the data in descending order by "total_powers"
```

## Your Favorite
9. Pick your favorite superhero and let's see their powers!  

```r
superhero_powers %>% 
  filter(hero_names == "Winter Soldier")
```

```
## # A tibble: 1 × 168
##   hero_names     agility accelerated_healing lantern_power_ring
##   <chr>          <lgl>   <lgl>               <lgl>             
## 1 Winter Soldier FALSE   FALSE               FALSE             
## # ℹ 164 more variables: dimensional_awareness <lgl>, cold_resistance <lgl>,
## #   durability <lgl>, stealth <lgl>, energy_absorption <lgl>, flight <lgl>,
## #   danger_sense <lgl>, underwater_breathing <lgl>, marksmanship <lgl>,
## #   weapons_master <lgl>, power_augmentation <lgl>, animal_attributes <lgl>,
## #   longevity <lgl>, intelligence <lgl>, super_strength <lgl>,
## #   cryokinesis <lgl>, telepathy <lgl>, energy_armor <lgl>,
## #   energy_blasts <lgl>, duplication <lgl>, size_changing <lgl>, …
```

10. Can you find your hero in the superhero_info data? Show their info!  

```r
superhero_info %>% 
  filter(name == "Winter Soldier")
```

```
## # A tibble: 1 × 10
##   name   gender eye_color race  hair_color height publisher skin_color alignment
##   <chr>  <chr>  <chr>     <chr> <chr>       <dbl> <chr>     <chr>      <chr>    
## 1 Winte… Male   brown     Human Brown         175 Marvel C… <NA>       good     
## # ℹ 1 more variable: weight <dbl>
```

## Knit and Upload
Please knit your work as a .pdf or .html file and upload to Canvas. Homework is due before the start of the next lab. No late work is accepted. Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  
