# Datenbank-Entwurf

## Entwurfsmethodik

### Abstraktionsebenen
Beim Entwurf kann man drei Abstraktionsebenen unterscheiden:

- Konzeptuelle Ebene - *Entity-Relationshio-Modell*
- Implementationsebene - *Relation, Tupel, Attribute*
- Physische Ebene - *Performance-Erhöhung mittels Indices. etc* 

### Anforderungsanalyse

- Identifikation von Organisationseinheiten
- Identifikation der hzu unterstützenden Aufgaben
- Anforderungs-Sammelplan
- Anforderungs-Sammlung
- Filterung
- Satzklassifikationen
- Formalisierung

### Objektbeschreibung

###### Hochschul-Angestellte (Anzahl: 1000)

- Attribut **PersonalNummer**
	- Typ: char
	- Länge: 9
	- Anzahl Wiederholungen: 0
	- Definiertheit (Wk für Belegung): 100%
	- Identifizierend: ja

- Attribut **Gehalt**
	- Typ: dezimal
	- Länge: 8, 2 Nachkommastellen
	- Anzahl Wiederholungen: 0
	- Definiertheit: 100%
	- Identifizierend: nein 

### Beziehungsbeschreibung prüfen

- Beteiligte Objekte:
	- Professor als Prüfer
	- Student als Prüfling
	- Vorlesung als Prüfungsstoff
- Attribute der Beziehung
	- Datum
	- Uhrzeit
	- Note
- Anzahl: 50.000 pro Jahr

### Prozessbeschreibung: *Zeugnisausstellung*

- Häufigkeit: halbjährlich
- benötigte Daten
	- Prüfungen
	- Studienordnungen
	- Studenteninformation
	- ...
- Priorität: hoch
- zu verarbeitende Datenmenge
	- 500 Studenten
	- 3000 Prüfungen
	- 10 Studienverordnungen

	
## ER-Modell

### Entity

> Als Entitäten werden wohlunterscheidbare (identifizierbare) physisch oder gedanklich existierende Konzepte der zu modellierenden Welt bezeichnet.

Entitäten unterscheiden sich von einander durch ihre Eigenschaften (Attribute( bzw. Eigenschaftswerte.

###### Beispiele:
bestimmte Personen, Firmen, Raumschiffe, etc.

### Entitäts-Typ

> Gleichartige Entitäten (Entitäten mit gleichen Eigenschaften, aber unterschiedlichen Eigenschaftswerten) werden zu Entitäts-Typen zusammengefasst (kategorisiert).

> Dabei sind nicht die Werte der Attribute, sondern deren Anzahl und Art der Eigenschaften für die Zusammenfassung entscheidend.

Bei der Modellierung werden nicht einzelne Entitäten, sondern der Entitäts-Typ, betrachtet.
Graphische Darstellung erfolgt durch ein Rechteck.

### Attribute

> Attribute bzw. Eigenschaften charakterisieren eine Entität, einen Entity-Typ, eine Beziehung bzw. einen Beziehungstyp.

Graphische Darstellung erfolgt durch eine Ellipse.

Attribute besitzen:

- einen Namen
- einen Wert


### Domäne
> Eine Domäne beschreibt den zulässigen Wertebereich einer Eigenschaft

###### Beispiele:
- fest vorgegebene Werte: Montag, Dienstag, ...
- Bereiche wie: 0,1,2 bis 10000; oder A-Z
- Datentypangaben wie: reele Zahl, ganze Zahl, etc.

### Beziehungen
> Beziehungen drücken die Wechselwirkung oder Abhängigkeit von Entitäten aus.

Beziehungen können, genau wie Entitäten, Eigenschaften (Attribute) besitzen.

### Beziehungs-Typ
> Der Beziehungs-Typ ist die Abstraktion gleichartiger Beziehungen. Das Verhältnis zwischen Beziehungstyp und Beziehun ist analog zum Verhältnis Entitätstyp zu Entität.

Graphische Darstellung erfolgt durch eine Raute.

### Schlüssel

> Eine minimale Menge von Attributen, die eine Entität eindeutig identifiziert, wird als Schlüssel bezeichnet.

Eine Entität wird durch die Kombination aller seiner Attributwerte eindeutig beschrieben, sonst wäre sie nicht unterscheidbar. Im Allgemeinen reicht jedeoch eine Teilmenge der Attribute aus, um eine Entität eindeutig zu beschreiben.

### Primärschlüssel
> Sind mehrere Schlüssel(-kandidaten) vorhanden, wählt man einen dieser Kandidaten als **Primärschlüssel** aus.

Manchmal sind "natürliche" Attribute ungeeignet, dann wird ein künstliches Attribut als Primärschlüssel hinzugefügt (Id).

Primärschlüssel werden durch Unterstreichen der Attribute im ER-Diagramm gekennzeichnet.

## Mengenlehre

Die Mengenlehre bildet die mathematische Grundlage der Theorie relationaler Datenbanken. Daher werden im Folgenden einige wesentliche Konzepte der Mengenlehre wiederholt.

### Menge
>Unter einer Menge verstehen wir jede Zusammenfassung $M$ von bestimmten, wohlunterschiedenen Objekten $e$ unserer Anschauung oder unseres Denkens (welche die Elemente von $M$ genannt werden) zu einem Ganzen.

Als Darstellung einer Menge kann man die Elemente $e_{i}$ der Menege $M$ aufzählen: $\{e_{1},e_{2},e_{3},e_{4\}}$

Dabei gilt:

- Reihenfolge der Elemente $ei$ spielt keine Rolle
- Mehrfach aufgezählte Elemente gelten nur einmal

$e_{i} \in M$ heißt: $e_{i}$ is Element der Menge $M$

### Teilmengen

$A$ und $B$ seien Mengen - dann steht $A  \subseteq B$ für:<br/>
$A$ ist Teilmenge von $B$: Jedes Element von $A$ ist auch Element von $B$.

### Kartesisches Produkt und Tupelbegriff

Das kartesische Produkt zwischen zwei Mengen $A$ und $B$ ist die Kombination aller Elemente zwischen den Elementen aus $A$ und $B$:<br/>
$A \times B = {(a,b)\mid a \in A \wedge b \in B} $

Durch das kartesische Produkt zwischen $A$ und $B$ wird eine Paar-Menge definiert.

Im Allgemeinen: $M_{1} \times M_{2} ... \times M_{n} =$<br/>
${(m_{1}, m_{2}, ... m_{n})\mid m_{1} \in M_{1}} \wedge m_{2} \in M_{2} ... m_{n} \in M_{n}$<br/>
Die Elemente des Produktes von $n$ Mengen heißen $n$-Tupel.

- $n=2$: Paare
- $n=3$: Tripel
- $n=4$: Quadrupel

### Tupelmengen und Relationen

>Jede Teilmenge eines Produktest $A_{1} \times A_{2} \times ... \times A_{n}$ heißt Relation über $A_{1} ... A_{n}$

Relationen können ebenso als Tabellen dargestellt werden.

$M_{1} = {D,B,C}$  
$M_{2} = {2,4,5,8}$  
$M_{3} = {m,w}$

| $M_{1}$ | $M_{2}$ | $M_{3}$ |
|---------|---------|---------|
| D | 2 | m |
| C | 5 | M |
| B | 8 | W |
| B | 4 | m |

### Partielle Funktionen

Gegeben seien zwei Mengen $A$ und $B$. Wenn jedem Element von $A$ genau ein oder kein Element aus $B$ zugeordnet wird, so kann dies als *partielle Funktion* aufgefasst werden. 
<center>
$f: X \to _{p} Y$  
</center>

Eine partielle Funktion ist eine *rechtseindeutige Relation*

## Funktionalitäten

### 1:1 Beziehung

<center>
$R \subseteq E_{1} \times E_{2}$
</center>

> Jedes Element aus $E_{1}$ kann mit maximal einem Element aus $E_{2}$ in Beziehung stehen. Außerdem skann jedes Element aus $E_{2}$ mit maximal einem Element aus $E_{1}$ in Beziehung stehen.

###### Beispiel
- verheiratet mit (zu einem Zeitpunkt - nach deutschem Recht)

Es gilt:  
$R: E_{1} \to _{p} E_{2}$ und $R: E_{2} \to _{p} E_{1}$

### 1:N Beziehung

<center>
$R \subseteq E_{1} \times E_{2}$
</center>

> Jedes Element aus $E_{1}$ kann mit beliebig vielen Elementen aus $E_{2}$ in Beziehung stehen und jedes Element aus $E_{2}$ kann mit maximal einem Element aus $E_{1}$ in Beziehung stehen.

###### Beispiel
- beschäftigen: (Firmen beschäftigen Personen)

Es gilt:  
$R: E_{2} \to _{p} E_{1}$

### N:1 Beziehung

<center>
$R \subseteq E_{1} \times E_{2}$
</center>

> Jedes Element aus $E_{2}$ kann mit beliebig vielen Elementen aus $E_{1}$ in Beziehung stehen und jedes Element aus $E_{1}$ kann mit maximal einem Element aus $E_{2}$ in Beziehung stehen.

###### Beispiel
- arbeitet bei: (Personen abreiten in Firma)

Es gilt:  
$R: E_{1} \to _{p} E_{2}$

### N:M Beziehung

<center>
$R \subseteq E_{1} \times E_{2}$
</center>

> Jedes Element aus $E_{1}$ kann mit beliebig vielen Elementen aus $E_{2}$ in Beziehung stehen und jedes Element aus $E_{2}$ kann mit beliebig vielen Elementen aus $E_{1}$ in Beziehung stehen. => Keine Einschränkungen

###### Beispiel
- belegen: (Studenten belegen Module)

Kann nicht als partielle Funktion ausgedrückt werden.

Es gilt:  
$R: E_{2} \to _{p} E_{1}$

### Integritätsbedingungen

Funktionalitäten stellen Integritätsbedingungen dar, d.h. diese Bedingungen gelten in der zu modellierten Welt als Gesetzmäßigkeiten.  
Sie gelten nicht rein zufällig für einen Datenbestand.