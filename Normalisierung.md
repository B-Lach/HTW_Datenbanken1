#Normalisierung

Schrittweises Optimieren der Vorhandenen Datenstruktur.

## 1. Normalform

> Eine Relation ist in der 1. Normalform, wenn alle zugrunde liegenden Attribute **atomare Werte** enthalten und ein **eindeutiger Primärschlüssel** gegeben ist.

**Beispiel**

Vor Anwendung der 1 NF:

|PersNr|Name|AbtNr|Abteilung|ProjektNr|Beschreibung|Zeit|
|------|----|-----|---------|---------|------------|----|
|1|Sophia Meier-Lorenz|1|Personal|2|Verkaufspromotion|83|
|2|Tatjana Hohl|2|Einkauf|3|Konkurrenzanalyse|29|
|3|Theodor Müller|1|Personal|1, 2, 3|Kundenumfrage, Verkaufspromotion, Konkurenzanalyse | 140, 92, 110
|4|Otto Richter|3|Verkauf|2|Verkaufpromotion|67|
|5|Hertha Wiesenland|2|Einkauf|1|Kundenumfrage|160|

Nach Anwendung der 1 NF:

|PersNr|Vorname|Nachname|AbtNr|Abteilung|ProjektNr|Beschreibung|Zeit|
|------|-------|--------|-----|---------|---------|------------|----|
|     1|  Sophia|Meier-Lorenz|1|Personal|2|Verkaufspromotion|83|
|     2| Tatjana| Hohl|2|Einkauf|3|Konkurrenzanalyse|29|
|     3| Theodor| Müller|1|Personal|1|Kundenumfrage |140|
|     3| Theodor| Müller|1|Personal|2|Verkaufspromotion|92|
|     3| Theodor| Müller|1|Personal|3|Konkurenzanalyse|110|
|     4|    Otto|Richter|3|Verkauf|2|Verkaufpromotion|67|
|     5|  Hertha|Wiesenland|2|Einkauf|1|Kundenumfrage|160|

*Erklärung:*

Name wurde aufgespaltet in Vorname, Nachname $\rightarrow$ Atomare Werte sichergestellt  
Primärschlüssel ist zusammengesetzt aus: PersNr + ProjektNr

## 2. Normalform

> Eine Relation ist in der 2. Normalform, wenn sie die Bedingungen der **ersten Normalform** erfüllt und jedes Nichtschlüsselattribut vom **gesamten** Primärschlüssel **voll funktional abhängig** ist.

Nach Anwendung der 2 NF:

*Mitarbeiter*

|PersNr|Vorname|Nachname|AbtNr|Abteilung
|------|-------|--------|-----|---------|
|     1|  Sophia|Meier-Lorenz|1|Personal|
|     2| Tatjana| Hohl|2|Einkauf|
|     3| Theodor| Müller|1|Personal|
|     4|    Otto|Richter|3|Verkauf|
|     5|  Hertha|Wiesenland|2|Einkauf|

*Erklärung:*

Primärschlüssel der neuen Relation: PersNr  
Alle Nichtschlüsselattribute, die voll funktional vom neu definierten PK abhängig sind, wurden in die neue Relation übertragen (Vorname, Nachname, AbtNr, Abteilung)

*Projekt*

|ProjektNr|Beschreibung|
|---------|------------|
|2|Verkaufspromotion|
|3|Konkurrenzanalyse|
|1|Kundenumfrage|
|2|Verkaufspromotion|
|3|Konkurenzanalyse|
|2|Verkaufpromotion|
|1|Kundenumfrage|

*Erklärung:*

Primärschlüssel der neuen Relation: ProjektNr  
Alle Nichtschlüsselattribute, die voll funktional vom neu definierten PK abhängig sind, wurden in die neue Relation übertragen (Beschreibung)

*Zeit*

|PersNr|ProjektNr|Zeit|
|------|---------|----|
|     1|2|83|
|     2|3|29|
|     3|1|140|
|     3|2|92|
|     3|3|110|
|     4|2|67|
|     5|1|160|

*Erklärung:*

Primärschlüssel der neuen Relation: PersNr + ProjekNr  
Alle Nichtschlüsselattribute, die voll funktional vom neu definierten PK abhängig sind, wurden in die neue Relation übertragen (Zeit)

## 3. Normalform

>Eine Relation ist in der 3. Normalform, wenn sie die Bedingungen der **zweiten Normalform** erfüllt und kein Nichtschlüsselattribut von einem Schlüsselattribut **transitiv abhängt** bzw. kein Nichtschlüsselattribut **von einem anderen Nichtschlüsselattribut abhängig** ist.

Nach Anwendung der 3 NF:

Die Relationen Zeit und Projekt befinden sich jeweils schon in der 3 Normalform, da jeder ihrer Nichtschlüsselattribute vom Primärschlüssel abhängt. Jedoch befindt sich in der Mitarbeiter Relationen ein Attribut, welches von einem Nichtschlüsselattribt abhängig ist (Abteilung)


*Abteilung*

|AbtNr|Abteilung|
|-----|---------|
|1|Personal|
|2|Einkauf|
|3|Verkauf|

*Erklärung:*

PK der Relation: AbtNr

AbtNr und deren Titel wurden in eine neue Relation ausgelagert.

*Mitarbeitet*

|PersNr|Vorname|Nachname|AbtNr|
|------|-------|--------|-----|
|     1|  Sophia|Meier-Lorenz|1|
|     2| Tatjana| Hohl|2|
|     3| Theodor| Müller|1|
|     4|    Otto|Richter|3|
|     5|  Hertha|Wiesenland|2|

*Erklärung:*

Da Abteilung in eine separate Relation ausgelagert wird, ist diese Information nicht mehr Bestandteil der Mitarbeiter Relation. Jedeglich die AbtNr wird weiterhin, jedoch nun als *Fremdschlüssel*, in der Relation festgehalten.