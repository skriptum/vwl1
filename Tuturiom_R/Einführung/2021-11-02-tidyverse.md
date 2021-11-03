# 02.11.02 Der Tidyverse Approach

```{r}
setwd("~/Nextcloud/vwl1/Tuturiom_R/Einführung")
```

Import -> Tidy -> Transform / Visualise / Model -> Communicate

### readr for import

```{r}
library("readr")
```

Paket zum importieren verschiedener Formate Import der Dateien (nur mit working directory in "Einführungs" Folder)

```{r}
#normal CSV
flights_csv <- read_csv("data/flights.csv")
#STATA
flights_dta <- read_dta("data/flights.dta")
#SPSS
flights_sav <- read_sav("data/flights.sav")
```

=> verschiedene praktische Sachen, alles auch im cheatsheet

### working with tidyr

```{r}
library("tidyr")
```

different functions to wrangle datasets and clean them

`gather`: gather columns into key value pairs

```{r}
help(gather)

#pipe the table into a function
table4a %>% 
  gather("1999","2000", key="year", value="cases")
```

`spread`: spread key value pair across columns

```{r}
help(spread)

#pipe the table into a function
table2 %>% 
  spread(key="type", value="count", convert = T)
```

`separate`: turn single character column into multiple columns

```{r}
table3 %>% 
  separate(rate, into = c("cases", "population"), convert = T)
```

`unite`: unit columns into one

```{r}
table5 %>% 
  unite("century", "year", col = "year", sep="")
```

### dplyr

Datentransformation mit *dplyr*

```{r}
library("dplyr")
library("nycflights13")
```

Einladen des Datensatzes `filter`: einzelne Zeilen aus dem Datensatz raúsziehen

```{r}
flights %>%
  filter(month == 1, day == 1)

flights %>%
  filter(arr_delay >= 60)
```

`arrange`: ordnen von Daten

```{r}
flights %>%
  arrange(dep_time)
```

`select`: einzelne spalten

```{r}
flights %>%
  dplyr::select(year : day)
```

`rename`: Umbenennung von Spalten namen

```{r}
dplyr::rename(flights, arriving = arr_time)
```

`mutate`: eurezugt neue Variable aus alten

```{r}
flights %>%
  dplyr::select(distance,air_time) %>%
  dplyr::mutate(speed = distance/air_time * 60)
```

`summarize` und `count`

```{r}
flights %>%
  dplyr::summarize(delay_average = mean(dep_delay, na.rm = T) )
```

`groupby` : Gruppieren von Daten

```{r}
flights %>% 
  group_by(carrier) %>%
  summarize(del_avg = mean(dep_delay, na.rm = T), 
            del_sd= sd(dep_delay, na.rm = T),
            del_median = median(dep_delay, na.rm = T)
            )
```

`join`: zusammenfügen verschiedener Datensätze

```{r}
flights %>%
  dplyr::select(carrier, dep_time) %>%
  left_join(airlines, by = "carrier")
```

### Aufgabenblatt

Starwars - Datensatz einladen

tidyr-arbeit: 
```{r}
load("data/starwars.RData")

#2 !Not finished
tidyr::unite(starwars2, "feminine", "masculine", col = "gender" , na.rm = T)

#3
tidyr::spread(starwars3, key=body_measure, value = body_values, convert = T)

#4 problems with doulbes and integers
tidyr::separate(starwars4, mass_height, into=c("mass", "height"),convert = T)

#5 
tidyr::unite(starwars5, hair_color1, hair_color2, col = "haircolor", na.rm = T, sep="-")
``` 

dplyr-arbeit:
```{r}
#1 
starwars %>%
  filter(mass > 75, mass < 100, height > 180, height < 190) %>%
  dplyr::select(name,eye_color)
  
#2 
starwars %>%
  filter(is.na(height) | is.na(height))
  
#3
dplyr::arrange(starwars, -desc(mass))
dplyr::arrange(starwars, desc(height))
#Darth Vader height = 202

#4
starwars %>%
  dplyr::filter(species != "Droid") %>%
  dplyr::filter(!is.na(height) , !is.na(mass)) %>%
  dplyr::select(name:mass) %>%
  dplyr::mutate(bmi = mass/((height/100)**2))

#5 
starwars %>% 
  dplyr::rename("größe" = "height" ) %>%
  rename("gewicht"= "mass") %>%
  rename("haarfarbe"= "hair_color" ) %>%
  rename("hautfarbe"= "skin_color")
  
#6
starwars %>%
  dplyr::filter(species != "Droid") %>%
  dplyr::filter(!is.na(height) , !is.na(mass)) %>%
  dplyr::select(name:mass) %>%
  dplyr::mutate(bmi = mass/((height/100)**2)) %>%
  dplyr::summarize(
    mass_mean = mean(mass),
    mass_median = median(mass),
    mass_sd = sd(mass),
    height_mean = mean(height),
    height_median = median(height),
    height_sd = sd(height),
    bmi_mean = mean(bmi),
    bmi_median = median(bmi),
    bmi_sd = sd(bmi),
  )
  
#7 
starwars %>%
  dplyr::filter(!is.na(height) , !is.na(mass)) %>%
  dplyr::select(name:mass, species) %>%
  dplyr::mutate(bmi = mass/((height/100)**2)) %>%
  dplyr::group_by(species) %>%
  dplyr::summarize(
    mass_mean = mean(mass),
    mass_median = median(mass),
    mass_sd = sd(mass),
    height_mean = mean(height),
    height_median = median(height),
    height_sd = sd(height),
    bmi_mean = mean(bmi),
    bmi_median = median(bmi),
    bmi_sd = sd(bmi),
  )
  
#8 
starwars %>%
  dplyr::filter(!is.na(height) , !is.na(mass)) %>%
  dplyr::select(name:mass, gender, species) %>%
  dplyr::mutate(bmi = mass/((height/100)**2)) %>%
  dplyr::group_by(gender, species) %>%
  dplyr::summarize(
    mass_mean = mean(mass),
    mass_median = median(mass),
    mass_sd = sd(mass),
    height_mean = mean(height),
    height_median = median(height),
    height_sd = sd(height),
    bmi_mean = mean(bmi),
    bmi_median = median(bmi),
    bmi_sd = sd(bmi),
  )
  
#9 
count(starwars, gender)
#10
dplyr::left_join(starwars6,starwars7, on = "name")

```
yeehaw, fertig