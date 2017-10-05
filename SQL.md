# SQL

> SQL unterscheidet **nicht** Groß- und Kleinschreibung. Ist damit *case insensitive*.

## Data Definition Language DDL
> Eine Datenbank ist ein Container für Tabellen (und weitere Datenbankobjekte)

### Wichtige DDL Befehle

```CREATE DATABASE``` - Erzeugen einer neuen Datenbank  
```ALTER DATABASE``` - Modifizieren einer Datenbank

```CREATE TABLE```- Erzeugen einer neuen Tabelle  

```sql
CREATE TABLE professoren(
	pers_nr INTEGER NOT NULL,
	name VARCHAR(20) NOT NULL,
	rang CHARACTER(2),
	raum INTEGER,
	PRIMARY KEY (pers_nr)
);
```

```ALTER TABLE``` - Modifizieren einer Tabelle  
```DROP TABLE``` - Löschen einer Tabelle

## Data Manipulation Language DML

### Wichtige DML Befehle

```ÌNSERT INTO``` - Einfügen neuer Daten

```sql
INSERT INTO professoren(pers_nr, name, rang, raum)
VALUES(2125, 'Sokrates', 'C4', 226);
```
```UPDATE``` - Ändern bestehender Daten
```DELETE``` - Löschen bestehender Daten

## Relationale Algebra

### Anfrageformulierung in relationalen Datenbanken

Zwei formale Sprachen als Grundlage für die Anfrageformulierung in relationalen Datenbanken:

- Relationale Algebra
- Relationenkalkül (rein deklarativ)

Mittels solcher Theorien (bzw. formaler Grundlagen) wird es möglich, exakte und nachweisbare Ausssagen über Datenbanken zu formulieren.

### Die ralationale Algebra

Formale Sprache für die Formulierung von Abfragen innerhalb eines relationalen Schemas

- ermöglicht Relationen miteinander zu verknüpfen oder zu reduzieren und daraus komplexere Informationen herzuleiten
- Definiert Operationen, die sich auf einer Menge von Relationen anwenden lassen
- Ergebnisse aller Operationen sind ebenfalls Relationen
- Relationale Algebra ist die Bases für die Datenbanksprache SQL

### Operationen der Relationenalgebra

$\sqcap$ Projektion  
$\sigma$ Selektion  
$\times$ Kreuzprodukt  
$\bowtie$ Join (Verbund)  
$\rho$ Umbennenung  
$-$ Mengendifferenz  
$\div$ Division  
$\cup$ Vereinigung  
$\cap$ Mengendurchschnitt  
$..$

### Weitere Operatoren der relationalen Algebra

$\ltimes$ Semi-Join (linker)  
$\rtimes$ Semi-Join (rechter)  
$⟗$ outer Join  
$⟕$ linker äußerer Join  
$⟖$ rechter äußerer Join

### Projektion
> Bei der Projektion werden die Attribute/Spalten einer (Argument-)Relation $R$ extrahiert. D.h. es sind nur die Attribute vorhanden, die ausgewählt wurden.

Projektions-Symbol: $\sqcap$  
Menge der Attributnamen im Subskript: $\sqcap _{Attributnamem}(Relationenname)$  
*Eventuell auftretende Duplikate werden entfernt*  
Beispiel: $\sqcap_{Rang}(Professoren)$  

```sql
SELECT rang FROM professoren;
```

### Selektion
> Bei der Selektion werden die Tupel einer Relation $R$ mittels eines $Selektionsprädikat$ gefiltert, d.h. das Ergebnis einer Selektion sind die Tupel der Relation $R$, die das Selektionsprädikat erfüllen.

Projektions-Symbol: $\sigma$  
Selektionsprädikat als Subskript: $\sigma _{Selektionsprädikat}(Relationenname)$  

Beispiel: $\sigma{Semester>10}(Studenten)$  

```sql
SELECT * FROM studenten
WHERE semester > 10;
```

### Duplikate
>Mathematische Relationen kennen keine Duplikate. In SQL Tabellen sind Duplikate aber erlaubt bzw. werden aus Effizienzgründen nicht automatisch beseitigt. Müssen explizit beseitigt werden.

```DISTINCT``` dient zur Beseitigung von Duplikaten

```sql
SELECT DISTINCT name from studenten;
```

### Kartesisches Produkt
> Das kartesische Produkt zwischen zwei Relationen $R$ und $S$ enthält alle $|R|*|S|$ möglichen Paare von Tupeln aus $R$ und $S$. Das Schema der Ergebnisrelation $sch(R \times S)$ ist die Vereinigung der Attribute aus $sch(R)$ und $sch(S)$.

Symbol: $\times$  
Verbindet zwei Relationen $R$ und $S: R \times S$
Ergebnisschema: $sch(R \times S)=sch(R) \cup sch(S)$

Beispiel: $Rrofessoren \times hoeren$

```sql
SELECT * FROM professoren, hoeren;

--Expliziter:
SELECT * FROM professoren
CROSS JOIN hoeren;
```

### Vereinigung
> Zwei Relationen mit dem gleichen Attributnamen und Attributtypen (Domänen) können durch Vereinigung zusammengefasst werden. In der Ergebnissrelation sind alle Tupel beider Mengen vorhanden.

Vereinigungssysmbol: $\cup$   
Verbindet zwei Relationen $R_{1}$ und $R_{2}$ mit gleichem (Attribut-)Schema: $R_{1} \cup R_{2}$  
Duplikatelemination

Beispiel: $\sqcap_{Name}(Professoren) \cup \sqcap_{Name}(Studenten)$

```sql
(SELECT name FROM professoren)
UNION
(SELECT name FROM studenten); 
```

### Differenz
> Zwischen zwei Relationen mit den gleichen Attributnamen und Attributtypen (Domänen) kann eine Mengen-Differenz gebildet werden. Dann sind in der Ergebnisrelation $D=A-B$ alle Tupel aus $A$ enthalten, die nicht in $B$ enthalten sind.

Symbol: $-$  
Verbindet zwei Relationen $A$ und $B$ mit gleichem (Attribut-)Schema: $D=A-B$  
Beispiel: $\sqcap _{MatrNr}(Studenten) - \sqcap _{MatrNr}(pruefen)$

```sql
(SELECT matr_nr FROM studenten)
EXPECT
(SELECT matr_nr FROM pruefen);
```

### Umbenennung
> BEi der Umbenennung einer Relation $R1$ zu den neuen Namen $R2$ wird eine "logische" Kopie der Relation erstellt. Auf die ursprüngliche Relation kann mit dem alten Namen $R1$ zugegriffen werden.

Symbol: $\rho$  
Vergibt für $R1$ den neuen Namen $R2: \rho_{R2}(R1)$  
Beispiel: $\rho_{Matrikelnummer}\leftarrow _{matr\_nr}(studenten)$

```sql
SELECT matr_nr FROM studenten
AS Matrikelnummer;
```