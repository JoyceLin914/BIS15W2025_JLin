---
title: "Homework 2"
author: "Joyce"
date: "2025-01-12"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and/or complete the exercises in RMarkdown. Please embed all of your code and push the final work to your repository. Your report should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run.  

**1. Objects in R are a way in which we can store data or operations. Make a new object `pi` as 3.14159. You should now see the object `pi` in the environment window in the top right.** 

```r
pi <- 3.14159
```

**2. Write a code chunk that divides `pi` by 2. Use the help command `?` to learn how to use the `round` function to limit your result to 3 significant digits.**  

```r
y <- pi/2
round(y,digits = 3)
```

```
## [1] 1.571
```

**3. Calculate the mean for the numbers 2, 8, 4, 6, 7, 4, 9, 9, 10. Please start by making a new object `x` that holds these values then use `mean` to perform the calculation.**  

```r
x <- mean(2, 8, 4, 6, 7, 4, 9, 9, 10)
x
```

```
## [1] 2
```

**4. Make five new vectors that show the name, height in feet, and height in meters of the five tallest mountains in the world.**

```r
name <- c("Mount Everest", "K2", "Kangchenjunga", "Lhotse", "Makalu")
feet <- c(29029, 28251, 28169, 27940, 27838)
meters <- c(8848, 8611, 8586, 8516, 8481)
```

**5. Combine these vectors into a data frame called `mountains`.**

```r
mountains <- data.frame(name, feet, meters)
```

**6. What is the mean height of the mountains in feet?**

```r
mean(feet)
```

```
## [1] 28245.4
```

**7. When were each of these mountains first climbed (i.e. in what year)? Make a new vector `first_climbed` and add it to the `mountains` data frame.**

```r
first_climbed <- c(1953, 1954, 1955, 1956, 1955)
mountains <- data.frame(name, feet, meters, first_climbed)
```

**8. How many times have each of these mountains been climbed? Make a new vector `summits` and add it to the `mountains` data frame.**

```r
mountains$summits <- c(11346, 355, 283, 300, 206)
```

**9. Which mountain has the highest number of fatalities? Make a new vector `fatalities` and add it to the `mountains` data frame.**

```r
mountains$fatalities <- c(322, 80, 58, 22, 31)
mountains
```

```
##            name  feet meters first_climbed summits fatalities
## 1 Mount Everest 29029   8848          1953   11346        322
## 2            K2 28251   8611          1954     355         80
## 3 Kangchenjunga 28169   8586          1955     283         58
## 4        Lhotse 27940   8516          1956     300         22
## 5        Makalu 27838   8481          1955     206         31
```

**10. Write your data frame to a .csv file.**

```r
write.csv(mountains, "mountains_data.csv", row.names = FALSE)
```

## Knit and Upload
Please knit your work as a .pdf or .html file and upload to Canvas. Homework is due before the start of the next lab. No late work is accepted. Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  
