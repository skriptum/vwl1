# 30.11.2021 Rücksendungen + Nachlässe



## Rücksendungen

(Video 17)

> **Rücksendungen:** entweder an Lieferanten oder von Kunden aufgrund von Mängeln

Ansprüche aufgrund von Mängeln:

- entweder Reperatur
- Austausch durch Neuprodukt
- wenn keine 2 Reparaturen oder keine Neulieferung:
    - Rücktritt vom Vertrag
    - Preisminderung

In Deutschland 2 Jahre Gewährleistungsdauer



### Buchung von Rücksendungen

`Rücksendungen sind wie Rückbuchungen!`

Beachten: Steuerberichtigung, Wertminderung



#### an Lieferanten

Beispiel: 

1. Einkauf von Rohstoffen auf Ziel (6000,-)
2. Rücksendung eines Teils der Leistung (900,-)

zu 1:

```
200 Rohstoffe             | 6000,-
260 Vorsteuer             | 600,-
an 44 Verbindlichkeiten   | 6600,-
```

zu 2: (**einfach Buchungssatz umdrehen**)

```
44 Verbindlichkeiten      | 990,-
an 200 Rohstoffe.         | 900,-
an 260 Vorsteuer          | 90,-
```



---

#### von Kunden

1. Verkauf von Fertigerzeugnissen auf Ziel (12.000€)
2. Beanstandung und Rücksendung eines Teils vom Kunden (3000€)

zu 1:

```
240 Forderungen       | 13 200,-
an 500 Umsatzerlöse   | 12 000,-
an 480 Umsatzsteuer   | 1 200,-
```

zu 2:

```
500 Umsatzerlöse      | 3000,-
480 Umsatzsteuer      | 300,-
an 240 Forderungen    | 3300,-
```



**Übung 7.4!**



### Nachlässe

> **Nachlass:** Preisminderung aufgrund von Mängelrügen 



#### im Einkauf

entweder als Netto- oder Bruttobuchung 

Beispiel: *wir erhalten vom Lieferanten Preisnachlass von 20% auf Rohstofflieferung (5000,-)*

```
Rohstoffpreis netto:       5000,-
   davon 20% Nettonachlass = 1000,-
+ Vorsteuer                500,-
   20% Steuerberichtigung  = 100,-
------------------------------------------
= Rechnungspreis (brutto)  5500,-
   Nachlass                = 1100,- 
```

Unterkonten :

- 200**2** Nachlässe für Rohstoffe
- 202**2** Nachlässe Hilfsstoffe
- ...

```haskell
1) einkaufsbuchung
200 Rohstoffe               | 5 000,-
260 Vorsteuer               | 500,-
an 44 Verbindlichkeiten     | 5 500,-
2) nettobuchung des nachlasses (20%)
44 Verbindlichkeiten        | 1 100,-
an 2002 Nachlässe Rohstoffe | 1 000,-
an 260 Vorsteuer            | 100,-
3) am monatsende: umbuchung der nachlässe
2002 Nachlässe Rohstoffe    | 1000,-
an 200 Rohstoffe            | 1000,-
```



