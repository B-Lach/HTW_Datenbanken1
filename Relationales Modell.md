# Relationales Modell

## Grundlagen

### Relation
Seien $D_{1}, D_{2},...,D_{n}$ Domänen (Wertebereiche)  
$D_{i} = D_{j}$ ist möglich  
Beispiele: Zahlen, Zeichenketten, Datum, boolsche Werte

>Eine Ralation $R$ ist definiert als Teilmenge des kartesischen Produktes der $n$ Domänen: $R \subseteq D_{1} \times\ ...\ \times D_{n}$

###### Beispiel
$Telefonbuch \subseteq string \times string \times integer$  
Der erste String steht für den Namen, der zweite für die Addresse und der Integer für die Telefonnummer.

### Relationenschema
Das **Relationen-Schema** legt die Struktur der gespeicherten Daten fest, z.B:  
$Telefonbuch: \{[Name: string, Address: string, \underline{Telefon\#: integer}]\}$ mit:

- Mengenoperator {..}
- Tupelkonstruktor [..]

### Tupel

Relation: $R \subseteq D_{1} \times\ ...\ \times\ D_{n}$

>Ein Element der Relation $R$ wird als Tupel bezeichnet. Seine Stelligkeit ist $n$.

$Tupel: t \in R$  
###### Beispiel
$t = ("Mickey Mouse", "Main Street", 4711)$

## Tabellen

### Relationen als Tabellen
Relationen können als Tabellen dargestellt werden:
<center>
	<table>
		<tr>
			<th colspan=3;">Telefonbuch</th>
		</tr>
		<tr>
			<th>Name</th>
			<th>Straße</th>
			<th>Telefon#</th>
		</tr>
		<tr>
			<td>Mickey Mouse</td>
			<td>Main Street</td>
			<td>4711</td>
		</tr>
		<tr>
			<td>Mini Mouse</td>
			<td>Broadway</td>
			<td>94725</td>
		</tr>
		<tr>
			<td>Donald Duck</td>
			<td>Highway</td>
			<td>93503</td>
		</tr>
		<tr>
			<td>...</td>
			<td>...</td>
			<td>...</td>
		</tr>
	</table>
</center>

Als **Ausprägung** wird dabei der aktuelle Zustand der Datenbasis bezeichnet.

### Tabellen

Eine Tabelle, wie die "Telefonbuch-Tabelle" besteht aus:  

- **Tabellen-Schema**
	- Die Tabelle hat einen Namen, dies entspricht dem Namen der Relation
	- Jede Spalte in der Tablle hat eine Spalteüberschrift (Name d. Tabelle; 	enspricht der Bezeichnung des Attributes 
- **Tabellen-Daten**
	- Einzelne Datensätze entsprechen den Zeilen der Tabelle
	- In den Spalten stehen dabei Were, die zum entsprechenden Attribut passen: 	Jeder Wert hat einen Datentyp


### Datentypen
> Ein (konkreter) Datentyp ist eine Menge von Werten und mit den darauf definierten Operationen.

Gänige Datentypen:

- Text
- Zahl
- Datum
- Boolean

###### Beispiel Ganze Zahlen

**Wertebereich:** mesit 32 Bit ($-2^{31}\ ...\ 2^{31}-1$), 16 Bit, 64 Bit  
**Operationen:** $+,-,*,<,>,=$, Division mit Rest und Modulo

### Datentypen für Attribute

Jedem Attribut (Spalte) wird ein Datentyp zugewiesen.
Der zugewiesene Datentyp bildet den Wertebereich (Domäne) des Attributs. Dabei sind noch weitere Einschränküngen möglich - z.B: A-D.  
<center>*Datentypen und Einschränkungen hängen von der zu verwendeten DBMS ab.*</center>

### Nullwerte
Attribute werden entspechend ihrem Wertebereich mit Werten belegt. Sie können aber auhch *undefiniert* bleiben, was durch den symbolischen Wert ```NULL``` ausgedrückt wird.

* ```NULL``` ist nicht mit der nummerischen 0 gleichzusetzen
* ```NULL``` kann nicht mit anderen Werten verglichen werden

## Relationale Modell

### Strukturelemente im ER-Modell und im ralationalen Modell
Im ER-Modell gibt es Entitätstypen und Beziehungstypen.  
Im relationalen Modell gibt es **nur** Relationen.

Sowohl Entitätstypen als auch Beziehungstypen werden als Relationen (Tabellen) repräsentiert.

### Relationale Darstellung von Entitätstypen

$Studenten: \{[\underline{MatrNr: integer}, Name: string, Semester: integer]\}$
$Vorlesungen: \{[\underline{VorlNr: integer}, Titel: string, SWS: integer]\}$
$Professoren: \{[\underline{PersNr: integer}, Name: string, Fachgebiet: string]\}$

### Fremdschlüssel
>Ein Fremdschlüssel ist ein Attribut in einer Relation, welches eine Beziehung zu einem Schlüsselfeld einer anderen Relation herstellt.

Fremdschlüssel dienen dazu Relationen zu verknüpfen.

## Verfeinerungen

### Ziele der Transformation des ER-Modells in ein relationales Modell

1. Bei der Füllung von Tabellen mit Daten sollen redundante Daten vermieden 	werden
2. Vermeiden von NULL-Einträgen in die Tabellen - soweit möglich
3. Unter Berücksichtigung von 1 und 2 soll Anzahl der Tabellen möglichst klein sein

### Zusammenfassen von Relationen
> Nur Relationen mit gleichem Schlüssel können zusammengefasst werden!

Wird die Regel nicht eingehalten, kommt es zu Anomalien.

### Anomalien

* Update-Anomalie
* Lösch-Anomalie
* Einfügeanomalie