# PostgreSQL

## Datentypen

PostgreSQL hat eine Vielzahl an Datentypen, die hier (nicht vollständig) tabellarisch dargestellt werden. Die im Detail [hier](http://www.postgresql.org/docs/current/interactive/datatype.html) nachgelesen werden können.

### Schemadefinition und Schemaveränderung

**```CREATE TABLE```**  

Anlegen von Tabellen inkl. der Möglichkeit Integritätsregeln zu definieren


**```ÀLTER TABLE```**  

Verändern von Tabellen, wie zum Beispiel das Hinzufüge von Attributen, Löschen von Spalten (```DROP COLUMN```), Ändern von Datentypen der definierten Attribute:

```sql
ALTER TABLE professoren
ALTER COLUMN name
TYPE varchar(50);
```

**```DROP TABLE```**

Löschen von Tabellen

## Sortierung

Projektionen können mittels ```ORDER BY``` sortiert werden. Dabei kann optional angegeben werden ob diese auf- bzw. absteigend sortiert werden sollen:

```ASC```: Aufsteigend sortieren (Standard)  
```DESC```: Absteigend sortieren

**Beispiel**:

Professoren-Tabelle geordnet nach Rang *(Hauptkreterium für Sortierung)* und Name *(Nebenkriterium für Sortierung)*:

```sql
SELECT * FROM professoren
ORDER BY rang desc, name asc
```

| pers_nr | name |rang|raum|
|---------|------|----|----|
|2136|Curie|C4|36|
|2137|Kant|C4|7|
|2134|Augustinus|C3|309|
2133|Popper|C3|52|

## Gruppierung

### Aggregatfunktionen
> Aggregatfunktionen dienen dazu Tupelmengen mittels einer Operation auf einen Wert abzubilden.

Aggregationfunktionen, die auf Zahlen operieren:

$avg$: Bestimmung des Durchschnitts  
$min$: Minimalwert  
$max$: Maximalwert  
$sum$: Bildung einer Summe  
$count$: Summe der Zeilen in einer Tabelle

**Beispiele**

Durchschnittliche Semesteranzahl:

```sql
SELECT avg(semester) FROM studenten;
```

Längste Studiendauer:

```sql
SELECT max(semester) FROM studenten;
```

Anazl aller Sutdenten:

```sql
SELECT count(*) FROM studenten;
```

### Gruppieren
> Mit $GROUP\ BY$ kann man Gruppen bilden, die mit Aggregatfunktionen ausgewertet werden können.

**Beispiel**

```sql
SELECT gelesen_von, sum(sws) FROM vorlesungen
GROUP BY gelesen_von;
```
#### Erlaubte Ergebnis-Spalten von *GROUP BY*

>Jede Gruppe wird nur durch ein einzelnes Tupel repräsentiert. Das heißt:  
>Alle in der Projektion verwendeten Attribute zur Erzeugung der Ergebnis-Relation müssen in der $GROUP\ BY$-Klausel angegeben werden.

Nur so kann sichergestellt weredn, dass sich der Attributswert nicht innerhalb der Gruppe ändert.

#### Bedingungen für Ergebnisrelation
Mit $HAVING$ lssen sich zusätzliche Bedingungen an die Gruppen stellen, d.h. hiermit können Gruppen der Ergebnisrelation ausgewählt werden.

**Beispiel**

```sql
SELECT gelesen_von, sum(sws) FROM vorlesungen
GROUP BY gelesen_von
HAVING avg(sws) >= 3;
```

#### WHERE vs. HAVING

> $WHERE$ filtert die einzelnen Zeilen der Agregationsreltionen (bzw. kartesisches Produkt der Ausgangsrelation). 
> $HAVING$ filtert die Gruppen - typischerweise bezüglich Aggregatsbedingungen.

**Beispiel**

```sql
SELECT gelesen_von, name, sum(sws) FROM vorlesungen, professoren
WHERE gelesen_von = pers_nr AND rang = 'C4'
GROUP BY gelesen_von, name HAVING avg(sws) >= 3;
```

## Relationskalkül

Bisher wurde die Relationsalgebra genutzt, die prozedurale Berechnungsvorschrift (vgl. Operatorbäume).  
Nun soll das Relationskalkül (deklarativ) basierend auf dem mathematischen Prädikatenkalkül erster Stufe, dem Existensquantor und Allquantor, genutzt werden.  

Die zwei Ausprägungen des Relationenkalküls lauten:

- relationales Tupelkalkül
- relationales Domänenkalkül

### Das Tupelkalkül

Eine Anftage im Tupelkalkül hat die Form
<center>
$\{t\ |\ P(t)\}$
</center>
$t$: Tupelvariable
$P$: Prädikat, welches erfüllt sein muss, damit $t$ Teil des Ergebnisses wird.

**Beispiel**
C4-Professoren
<center>
$\{\ p\ |\ p \in Professoren \wedge p.Rang = 'C4'\ \}$
</center> 

### Beispeiel für die Anwendung des Existenzquantors

Studenten, die mindestens eine Vorlesung hören:

$\{s\ | s \in Studenten \wedge \exists h \in hören(s.MatrNr=h.MatrNr)\}$

```sql
SELECT s.* FROM studenten s
WHERE EXISTS
(SELECT h.* FROM hoeren h 
WHERE s.matr_nr = h.matr_nr);
```

**Komplexeres Beispiel**

Studenten, die mindestens eine Vorlesung von Sokrates hören:

$\{s\ |\ s \in Studenten$  
$\ \ \ \ \ \ \ \ \ \wedge \exists h \in hören(s.MatrNr=h.MatrNr$  
$\ \ \ \ \ \ \ \ \ \wedge \exists v \in Vorlesungen(h.VorlNr=v.VorlNr$  
$\ \ \ \ \ \ \ \ \ \wedge \exists p \in Professoren(p.PersNr = v.gelesenVon$  
$\ \ \ \ \ \ \ \ \ \wedge p.Name = 'Sokrates')))\}$  

```sql

 SELECT s.* FROM studenten s WHERE EXISTS
   (SELECT h.* FROM hoeren h WHERE
    s.matr_nr = h.matr_nr AND EXISTS
     (SELECT v.* FROM vorlesungen v WHERE
      h.vorl_nr = v.vorl_nr AND EXISTS
       (SELECT p.* FROM professoren p WHERE
        p.pers_nr = v.gelesen_von AND
        p.name = 'Sokrates')));
```

### Alquantor

Wer hat **alle** vierstündigen Vorlesungen gehört:

$\{s\ |\ s \in Studenten \wedge \forall v \in Vorlesungen(v.SWS = 4 \Rightarrow$  
$\ \ \ \ \exists h \in hören(h.VorlNr = v.VorlNr \wedge h.MatrNr = s.MatrNr))\}$

## Schachelung

In SQL können SELECT-Anweisungen auf verschiedenste Weise verbunden und geschachtelt werden.
>Der SQL-Standard fordert, dass Unteranfragen geklammert werden.

Unteranfragen können dabei in allen drei Teilen einer SELECT-Anweisung stehen, dh. im SELECT-, FROM- und WHERE-Teil

### Unkorrelierte Unterfragen

>Unkorreliert Unterfragen benutzen lediglich ihre "eigenen" Attribute.

Unkorrelierte Unteranfragen müssen nur einmal ausgewertet werden.

**Beispiel**

```sql
SELECT * FROM pruefen 
WHERE note <= (SELECT avg(note) from pruefen);
```

### Korrelierte Unteranfragen
> Korrelierte Unteranfragen benutzen auch Attribute übergeordnerter Anfragen

Korrelierte Unteranfragen müssen i.A. für jedes Tupel der übergeordneten Anfrage ausgewertet werden ("nested-loop"-Semantik).

**Beispiel**

```sql
SELECT p.pers_nr, p.name, (SELECT sum(sws) FROM
vorlesungen v WHERE v.gelesen_von = p.pers_nr) AS
lehrbelastung FROM professoren p;
```

### Korrelierte vs unkorreliert

```sql
SELECT * from studenten s WHERE EXISTS 
(SELECT p.* from professoren p
WHERE p.geb_datum > s.geb_datum);
```

VERSUS

```sql
SELECT * from studenten s 
WHERE s.geb_datum < (SELECT
max(p.geb_datum) from professoren p);
```

- unkorellierte Unteranfragen sind effizienter
- Heutige Anfrageoptimierer sind i.A. nicht in der Lage korrelierte Unteranfragen selbst zu entkorrelieren

> Korrelierte Unteranfragen sollen us Effizeinzgründen vermieden werden. Durch manuelle Umformulierungen lassen sich korrelierte Unteranfragen oft in unkorrelierte umformen, so lässt sich die Leistungsfähigkeit *(performance)* einer Datenbankanwendung erhöhen.

## Mengenoperatoren

Bekannte Mengenoperatoren: ```UNION```, ```INTERSECT```, ```EXCEPT```  
Der Operator ```IN``` testet auf Mengenmitgliedschaft (in WHERE-Klausel).  
Komplementär zu ```IN```: ```NOT IN```  

**Beispiel**

```sql
-- Wähle alle Professoren, die keine Vorlesungen halten
SELECT name FROM professoren
WHERE pers_nr NOT IN
(SELECT gelesen_von FROM vorlesungen);
```

### ANY, ALL

```ANY``` wird genutzt um zu testen, ob mindestens ein Element des Ergebnisses der Unteranfrage einen Vergleich erfüllt - enspricht dem ```IN```-Operator.

```sql
SELECT * FROM kunden WHERE rating > any(
SELECT rating FROM kunden
WHERE stadt = 'Berlin');
```

```ALL``` wird genutzt um zu testen, ob alle Elemente des Ergebnisses der Unteranfrage einen Vergleich erfüllen.  
*Keine All-Quantifizierung möglich: Finden der Studenten, die alle 4-stündigen Vorlesungen hören geht nicht.*

```sql
SELECT name FROM studenten
WHERE semester >= all(
SELECT semester FROM studenten);
```