# R Tutorium

Alle Sachen hochgeladen über [ILIAS](https://ilias.uni-halle.de/goto.php?target=crs_219883&client_id=unihalle)
Format: Online Videos und Übungsaufgaben als PDF


--- 
# 27.10.21 Pakete und Datentyp
### Packages

Packages: R benutzt zur erweiterung von Funktionen bestimmte Packages, die Nutzer hochladen können

Installation: `install.package("tidyverse")`

Updaten: `update("tidyverse")`

Nutzung in Programmcode: `library("tidyverse")`

### R-Markdown

R-Markdown = Syntax von Markdown mit eingebauten Ausfürhungsmöglichkeit
Beispiel:
```{r}
x = 10
```
=> zum Beunutzen Zeile Markieren und CMD+Enter 


### Installation von wichtigen Paketen für diese Woche

Installation der Pakete
```{r}
install.packages(c("haven", "tidyverse"))
```
Laden in die Session
```
library("tidyverse")
library("haven")
```

## Datentypen

Abfragen des Types einer Variable:
```
mode(10)
```
-->Output: `numeric`


Leere Menge: `y <- NULL` oder `x <- c()`

#### Numerisch
entweder **integer** (natürliche Zahl) oder **double** (reelle Zahl)
 ```{r}
x <- 5.5
mode(x) # out: numeric
typeof(x) # out: double

## Integers: komplizierter
y <- as.integer(3)
typeof(y) # out: integer
```

#### Character
Zeichenkette, wie *string* in python

```{r}
z <- "Hallo"
mode(y) # out: character
```

#### logical
logische Werte, wie TRUE, FALSE bzw. T oder F und NA (not available)
TRUE = 1
FALSE = 0
praktisch für Statistische Analysen, bspws Anzahl TRUE einfach `sum()`

```{r}
is.numeric(x) #out: TRUE
is.character(x) #out: FALSE
```

#### Veränderung von Datentypen
Datentypen lassen sich in andere Datentypen umwandeln
```{r}
x <- as.character(x) 
x # out: '5.5'
x <- as.numeric(x)
x # out: 5.5
```
Datentyp beeinflusst, welche Funktionen angewendet werden können, und was kombiniert werden kann!


#### vektor
werden erstellt mit `c()` (combine)
```{r}
x <- c(1,2,3)
mode(x) # out: 'numeric'
y <- c(5,"a")
y # out: ('5', 'a')
```
alle Elemente eines Vektors müssn gleichem Datentyp zugehören. Ein char in einem Vektor macht also alles andere auch zu Vektoren

Indizierung von Vektoren
```{r}
x[2] #zweiter Wert out: 2
x[c(TRUE,FALSE,TRUE)] #out: 1 3
```
**!! Achtung nicht 0-index !!**

#### Matrizen 
erzeugt mithilfe der `matrix()`
```{r}
m <- matrix(1:6, ncol = 2) # 2 Spalten
# Matrix wird damit per Spalte besetzt
m <- matrix(1:6, ncol = 2, byrow = T)
m<- matrix(1:6, nrow = 3)
```

Indizierung von Matrizen mit [Zeile, Spalte]

```{r}
m[1,1] #: 1
m[2,] # 2  5 (gesamte zweite spalte )
```

wichtige Funktionen: 
Transponieren: `t(m)`
Diagonale: `diag(m)`

und wie bei Vektoren: alle Elemente selber Datentyp

#### Arrays
Ähnlich wie Matrizen , nur dimension > 2
```{r}
x <- array(1:12, dim = c(2,3,2))
x[2,2,1]
```
Indizierung Hier: [Zeile,Spalte,Element]

#### Liste

```{r}
a <- list(4,"a",c(8,8,8)) 
```
Liste kann beliebige andere Objekte, auch unterschiedlicher Länge / Art speichern
Indizierung mit `a[[2]]` -> `'a'`

#### DataFrames
eine Art der besonderen Liste mit extra Funktionen, 
muss aber gleiche Länge haben! wie `pandas.DataFrame()`
```{r}
x <- data.frame(hersteller,mpg$cyl) # 2 Zeilen gleichen Datensatzes
```

#### Tibbles
neue Art von Datentyp,
Dataframe nur noch fancier, noch mehr funktionen
```{r}
tibble()
```
mpg ist ein Tibble 
Indizierung mit $ oder `mpg[["year"]]

## Operatoren 
#### Vergleichs-operatoren
- == Gleichheit
- != Ungleichheit
- \>, >= Größer / Größer Gleich
- \<, <= Kleiner / Kleiner Gleich
- ! Nicht

Beispiel
```{r}
5 < 3 # out: FALSE
```
#### logische Operatoren

& : AND
| : OR
! : NOT
&& : AND, aber immer nur auf erste Elemente der Vektoren werden verglichen
|| : OR, aber auch nur erste Elemente

Beispiel
```{r}
1 & 1 # TRUE
1 | 0 # TRUE
0 | 0 # FALSE

a <- c(TRUE, FALSE, FALSE)
b <- c(FALSE, TRUE, TRUE)
a && b # FALSE, da nur TRUE und FALSE verglichen
a || b # TRUE

```



## Datenarbeit 

wir nutzen den datensatz `mpg` aus *tidyverse*

```{r}
mpg <- mpg
head(mpg) # first 10 rows

#Vektor Hersteller
hersteller <- mpg$manufacturer
```
Dollarsign = einzelne Spalte des Tibbles / DataFrames

Prüfen, ob irgendwas NAs enthält
```{r}
table(is.na(hersteller)) #out: FALSE 234

# Test mit Jahr
year <- mpg$year
table(year > 2000) #out: FALSE 117 ; TRUE 117
sum(year > 2000) #out: 117
```

Übung: 

```{r}
usa <- USArrests

##1
#a)
mode(usa$Murder)
#b)
usa$Murder <- as.character(usa$Murder)
#c)
state <- usa[0]
rownames(usa) <- NULL
#d)
usa_m <- as.matrix(usa) #Alles wird zum Character
usa_tibble <- as.tibble(usa) # Nichts aendert sich
#e) in listof-list umwandeln ?!!!
as.list(as.data.frame(t(usa))) 
```

Lösung für e) gefunden [hier](https://stackoverflow.com/questions/3492379/data-frame-rows-to-a-list)