# Grundlagen

## Daten - Syntaktische Ebene
- Zeichen (a-z, A-Z, 0-9)
- Zeichenvorrat + Syntax (Regeln) = Daten
- z.B- Datenelement vom Typ ```Integer``` = 181

## Information - Semantische Ebene
- Bedeutung verschiedener Datenelement (Interpretation der. Datenelemente)
- z.B. 181 ist die Größe on Herrn Mustermann in ```cm```

## Wissen - pragmatische Ebene 
- kontextspezifische Anwendung von Information (und Daten) für einen Zweck
- z.B. Berechnen der Durchschnittsgröße zur Konstruktion einer Parkbank

## Definitionen

### Datenbankverwaltungssystem (DBMS)
> Die Gesamtheit der Programme zum Zugriff auf die Datenbasesis, zur Kontrolle der Konsistenz und zur Modifikation der Daten, wird als *Datenbankverwaltungssystem (DBMS)* bezeichnet

### Datenbasis
> Eine *Datenbasis* ist eine Menge von Daten, die aus Sicht der Systembetreiber als zusammengehörig betrachtet werden.

### Datenbank
>Die Datenbasis angereichert um weitere Daten, die das DBMS zur Erfüllung seiner Aufgabe benötigt, bilden eine *Datenbank (DB)*

### Datenbanksystem
Eine DBMS einschließlich einer oder mehrerer Datenbanken nennt man ein *Datenbanksystem (DBS)*

## Motivation

Probleme, die den Einsatz eines DBMS adressiert:

- Redundanz und Inksonsistenz
- Beschränkte Zugriffsmöglichkeiten, keine Verknüpfung der Daten
- Probleme beim Mehrbenutzerbetrieb
- Verlust der Daten
- Integritätsverletzungen
- Sicherheitsprobleme / Datenschutzprobleme
- hohe Entwicklungskosten für Anwenderprogramme

## Abstraktion

Schichten gewährleisten einen bestimmten Grad der Datenunabhängigkeit

- Pyhische Datenunabhängigkeit
- Logische Datenunabhängigkeit

### Physische Ebene
Beschreibt, wie die Daten gespeichert werden

### Logische Ebene
Welche Daten und wie diese Daten logisch organisiert werden - *Datenbankschema*

### Sichten
Teilmenge der Gesamtdaten für einzelne Anwender(gruppen)

# Datenmodelle

## Modellierung

- Ausgangpunkt
	- reale (oder fiktive) Welt
	- wirtschaftliche / technische Problemstellung
- Analyse
	- Identifikation des Ausschnittes der Welt, der für die Problemstellung relevant ist
- (konzeptionelle) Modellierung des Ausschnitts
	- Modellierungsprachen - grapische Darstellung
	- Beispiel: Entity-Relationship Modell, UML

## Vorgehen

- Abbildung der Modellierung in das relationale Modell
	- technisch sind dies Tabellen
	- => welche Tabellen es gibt und aus welchen Spalten (ink. Namen d. Spalten) bestehen diese
	- Entspricht dem **Datenbank-Schema**
	- allgemeiner mittels der *Data Definition Langauge DDL*
- Füllen des Schemas mit den Daten der "realen" Welt
	- eigentliche Datenmanipulationssprache DML
- Nutzen der Daten mittels einer "Anfragesprache" - Teil der Datenmanipulationssprache
	- Anfragen (Queries)
	- Erstellen von Reports

## Das relationale Datenmodell

### Abfrage-Syntax


```sql
SELECT Name
FROM Studenten, hören, Vorlesungen
WHERE Studenten.MatrNr = hören.MatrNr AND
	  hören.VorlNr = Vorlesungen.VorlNr AND
	  Vorlesungen.Titel = 'Grundzüge';
```
```sql
UPDATE Vorlesungen
SET Titel = 'Grundzüge der Logik'
WHERE VorlNr = 5001;
```

<div>
<table style="float:left; margin-right: 5px;">
	<tr>
		<th colspan=2>Studenten</th>
	</tr>
	<tr>
		<th>MatrNr</th>
		<th>Name</th>
	</tr>
	<tr>
		<td>26120</td>
		<td>Fichte</td>
	</tr>
	<tr>
		<td>25403</td>
		<td>Jonas</td>
	</tr>
</table>

<table style="float:left; margin-right: 5px;"">
	<tr>
		<th colspan=2>hören</th>
	</tr>
	<tr>
		<th>MatrNr</th>
		<th>VorlNr</th>
	</tr>
	<tr>
		<td>25403</td>
		<td>5022</td>
	</tr>
	<tr>
		<td>26120</td>
		<td>5001</td>
	</tr>
</table>

<table style="float:left;">
	<tr>
		<th colspan=2>Vorlesungen</th>
	</tr>
	<tr>
		<th>VorlNr</th>
		<th>Titel</th>
	</tr>
	<tr>
		<td>5001</td>
		<td>Grundzüge</td>
	</tr>
	<tr>
		<td>5022</td>
		<td>Glaube uns Wissen</td>
	</tr>
</table>

