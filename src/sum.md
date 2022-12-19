# Zusammenfassung Typescript

Typescript ist eine Sprache, welche von Microsoft entwickelt wurde, um die Arbeit mit Javascript zu vereinfachen und Javascript um Datentypenannotationen erweitert.
Die Sprache wird, um sie für Browser verständlich zu machen, in Javascript umgewandelt.


## Grundlegende Konzepte und Syntax

### 1. Variablen

Ähnlich zur Mathematik lässt sich einer Variablen ein Wert zuweisen.
Variablen können verschiedene Arten von Werten darstellen, diese Arten von Variablen werden **Typen** genannt.
Javascript stellt bereits eingebaute Typen zur Verfügung. Einige der wichtigsten Typen sind in der folgenden Tabelle aufgelistet.

Typ       | Beschreibung
--------- | ----------------------------------
`string`  | beliebiger Text
`number`  | Dezimalzahl
`boolean` | Wahrheitswert `true` oder `false`

```typescript
// Variablen werden in Typescript meistens mit `let` und einem Namen deklariert:
let name: string = "Hans";
let wohnort: string = "Deutschland";
let alter: number = 25;
let abiturschnitt: number = 2.8;

// der Typ der Variablen kann in den meisten Fällen von der Sprache bestimmt werden
// und muss nicht angegeben werden
let verheiratet = false; // type: boolean

// nachdem eine Variable mit let deklariert wurde, kann ihr ein neuer Wert mit
// <name> = <wert> zugewiesen werden
alter = 26;
// da Befehle in Javascript und vielen anderen Sprachen
// von oben nach unten ausgeführt werden, beträgt der Wert der Variablen
// `alter` ab der Deklaration in der ersten Zeile `25`
// und ab dem Zuweisen des neuen Alters `26`
```
```typescript
// Variablen können, wie in der Mathematik, in Rechenoperationen verwendet werden
// in Javascript werden für die grundlegenden Operationen
// die Zeichen `+`, `-`, `*`, `/` verwendet:
let jahreErwachsen = alter - 18; // => 7
let restlicheLebenserwartung = 78.5 - alter; // => 53.5

// zu den Rechenoperationen können Werte verglichen werden
// für die Vergleiche können folgende Operatoren genutzt werden
//    `>`:   ist größer als
//    `<`:   ist kleiner als
//    `>=`:  ist größer oder gleich
//    `<=`:  ist kleiner oder gleich
//    `===`: ist gleich
//    `!==`: ist ungleich
// diese Vergleiche liefern einen `boolean`, je nachdem ob die Aussage
// wahr (true) oder falsch (false) ist
let kannMedizinStudieren = abiturschnitt < 1.2; // => false

// strings können ebenfalls verglichen werden, allerdings nur
// mit `===` und `!==`
let heisstPeter = name === "Peter"; // => false

// um mehrere Kriterien zu überprüfen, können
//     `a && b` als a und b treffen zu
// und `a || b` als a oder b treffen zu verwendet werden
let darfAlkoholKaufen = (wohnort === "Deutschland" && alter >= 16)
                     || (wohnort === "Amerika"     && alter >= 21); // => true

// tldr: Variablen können Werte besitzen
//       und in Rechnungen und Vergleichen verwendet werden
```

### 2. Kommentare
Kommentare erlauben es, dem Code Zusatzinformationen anzufügen, die das Geschriebene erklären, allerdings nicht ausgeführt werden.
Kommentare beginnen mit `//` und nehmen den Rest einer Zeile ein
```javascript
// das ist ein Kommentar

let test = 123; // das ist auch ein Kommentar
```

### 3. Funktionen
Funktionen können, wie in der Mathematik, Parameter annehmen und einen Wert produzieren.
Eine Javascript Funktion wird wie der restliche Code von oben nach unten ausgeführt.
Funktionen werden in Javascript mit `function` und einem Namen deklariert.
Die Eingabetypen der Funktion müssen im Gegesatz zu Variablentypen angegeben werden.
```typescript
// Eine Funktion mit dem Namen `f` welche eine Zahl quadriert
function f(x: number): number {
    // `return` bestimmt den Rückgabewert der Funktion
    // und bricht die Ausführung der Funktion ab
    return x * x;
    console.log("das hier wird niemals ausgeführt");
}

// eine Funktion kann, wie in der Mathematik,
// mit <name>(...<argumente>) aufgerufen werden
let a = f(2); // => 4
```

Javascript selbst bietet auch eingebaute Funktionen. Einige davon sind im Folgenden aufgelistet.
```typescript
// gibt `Hallo!` und die Zahl 123 auf die Browserkonsole aus
console.log("Hallo!", 123);

// liefert die Wurzel aus der Eingabezahl
let laenge = Math.sqrt(3*3 + 4*4); // => 5
// Math beinhaltet auch weitere mathematische Funktionen wie sin, cos, ...
```

### 4. Konditionale Ausführung (If / Else)
Mithilfe von `if` und `else` Blöcken kann je nach dem, welche Bedingungen zutreffen,
unterschiedlicher Code ausgeführt werden.
```typescript
let uhrzeitStunden = 13;

if(uhrzeitStunden > 12) {
    // da `uhrzeitStunden > 12` zutrifft, wird diese Zeile ausgeführt
    console.log("nachmittag");
} else {
    // diese Zeile wird übersprungen
    console.log("vormittag");
}
```

### 5. Wiederholte Ausführung (Schleifen)
`while` und `for` Schleifen erlauben es, in Javascript Code variabel oft
zu wiederholen ohne diesen mehrfach schreiben zu müssen.
```typescript
// `while` Schleife
// => prüft vor jedem Durchlauf, ob der Ausdruck in den Klammern === true ist
// diese Schleife wird unendlich lange ausgeführt
while(true) {
    console.log("Hallo!");
}

// `for` Schleife
//  => startet mit i = 0 (let i = 0) 
//     prüft vor jedem Durchlauf, ob i < 10 ist (i < 10)
//     erhöht i bei jedem Durchlauf um 1 (i++ kurz für i = i + 1)
for(let i = 0; i < 10; i++) {
    console.log("Hallo! - " + i);
}
```

### 6. Listen (Arrays)
Listen können beliebig viele Elemente von einem Typen enthalten.
```typescript
let rucksackInhalt = ["Powerbank", "Laptop", "Flammenwerfer"]; // type: string[]

// ein Element kann aus einer Liste extrahiert werden,
// indem in eckigen Klammern der Index eines Elements angegeben wird;
// ! der index einer Liste startet bei 0 !
let ersterGegenstand = rucksackInhalt[0]; // => "Powerbank"
// Elemente einer Liste können auch modifiziert werden
rucksackInhalt[1] = "Tablet";
// rucksackInhalt => ["Powerbank", "Tablet", "Flammenwerfer"]

// die Methode `push` fügt dem Array ein Element `Ladekabel` am Ende hinzu
rucksackInhalt.push("Ladekabel");
// rucksackInhalt => ["Powerbank", "Laptop", "Flammenwerfer", "Ladekabel"]

// mit einer `for` Schleife können alle Elemente einer Liste durchlaufen werden
for(let i = 0; i < rucksackInhalt.length; i++) {
    console.log((i + 1) + ". Gegenstand: " + rucksackInhalt[i]);
}
```

### 7. Klassen
Eine Klasse kombiniert Daten mit Funktionalität.
```typescript
// Klassen können mit `class` und einem Namen deklariert werden
class Schueler {
    // die "Felder" einer Klasse beschreiben die Daten
    // die mit jedem Objekt verbunden sind
    name: string;
    geburtsjahr: number;
    notendurchschnitt: number;
    geschlecht: string;

    // der Konstruktor ist eine besondere Methode welche die Daten
    // eines Objekts der Klasse initialisiert
    // ein Konstruktor wird mit `new` aufgerufen
    constructor(
        // der Konstruktor kann wie jede andere Methode Argumente akzeptieren
        name: string, geburtsjahr: number,
        notendurchschnitt: number, geschlecht: string,
    ) {
        this.name = name;
        this.geburtsjahr = geburtsjahr;
        this.notendurchschnitt = notendurchschnitt;
        this.geschlecht = geschlecht;
    }

    // Methoden einer Klasse funktionieren ähnlich wie gewöhnliche Funktionen
    // allerdings kann mit `this` auf das aktuelle Objekt
    // und somit auf die Daten von diesem Objekt zugegriffen werden
    getAlter(jahr: number): number {
        return jahr - this.geburtsjahr;
    }
}

// mit `new` wird ein neues Objekt vom Typ `Schueler` erzeugt
// der Konstruktor erhält die Argumente in den Klammern
let marie = new Schueler("Marie", 2005, 2.3, "w");

// auf dem konstruierten Objekt können Methoden
// mit <obj>.<methode>() aufgerufen werden
let alter = marie.getAlter(2022);

// mit <obj>.<feldname> kann dazu direkt auf ein Feld
// eines Objekts zugegriffen werden
let name = marie.name;
```

.
