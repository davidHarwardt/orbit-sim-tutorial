# Erzeugen der Canvas

## Code zum Erzeugen der Canvas
Die Canvas wird wie folgt erzeugt und direkt der Seite (`document.body`) hinzugefügt:
```typescript
let canvas = Canvas2d.fromParent(document.body);
canvas.addPlugin(new CanvasFullscreenPlugin());
// Platz für weitere Plugins
// ...
// -------------------------
canvas.init();
```
Außerdem wird der Canvas ein `CanvasFullscreenPlugin` hinzugefügt, damit sie den vollen Raum des Browserfensters ausfüllt.
Nachdem alle Plugins hinzugefügt wurden, wird die Canvas mit `init` initialisiert.

Anschließend muss ein `DrawLoop` erzeugt und gestartet werden, welcher die `draw` Funktion zyklisch aufruft (ca. 60 mal pro Sekunde).
```typescript
let loop = new DrawLoop(draw);
loop.start();
```

> Der Code kann mit Ctrl-S gespeichert werden.

## Das Koordinatensystem
Im Gegensatz zu herkömmlichen Koordinatensystemen ist die Y-Achse der verwendeten Canvas invertiert
und der Ursprung (also [0, 0]) liegt in der oberen, linken Ecke.
```
Die Koordinatensystem sieht also wie folgt aus:

    |(0, 0)                             (w, 0)
   -+--------------------------------------> x
    |
    | (100, 100)
    |      x---------+
    |      |         |
    |      |         |
    |      +---------+
    |
    |              (300, 300)
    |                   x
  y |
    V
 (0, h)
```

## Zeichnen von simplen Formen
Um Formen auf der Canvas zu zeichnen, muss dies in der `draw` Funktion stattfinden.
Damit die Canvas jeden Frame neu gezeichnet wird, muss zuerst die `clear` Methode der `canvas` aufgerufen werden,
gefolgt von `canvas.beginDraw();`.
Der Frame wird mit einem Aufruf von `canvas.endDraw();` beendet.

Die gesamte `draw` Funktion sollte wie folgt aussehen:
```typescript
function draw() {
    canvas.clear();
    canvas.beginDraw();

    // alle Zeichenfunktionen werden hier aufgerufen
    // ...
    // ---------------------------------------------

    canvas.endDraw();
}
```

Formen können nun mit den `drawXXX` Methoden der `canvas` gezeichnet werden.
Die Methoden benötigen Argumente, um die Form zu beschreiben (z.B. Kreis: Mittelpunkt und Radius).
Außerdem akzeptieren die Methoden ein letztes Argument um visuelle Eigenschaften der Form zu ändern
die Formen besitzen allerdings bereits Standardwerte für ihr Aussehen.

Form     | Methode      | Argumente                      | Style-Argumente
-------- | ------------ | ------------------------------ | ----------------------------------
Kreis    | `drawCircle` | `center: Vec2, radius: number` | `color: Color, ...`
Rechteck | `drawRect`   | `pos: Vec2, dim: Vec2`         | `color: Color, ...`
Linie    | `drawLine`   | `start: Vec2, end: Vec2`       | `width: number, color: Color, ...`
Text     | `drawText`   | `text: string, pos: Vec2`      | `size: number, color: Color, ...`

Punkte und Vektoren lassen sich mit einem `Vec2` beschreiben, welcher mit `new Vec2(<x>, <y>)` konstruiert werden kann.

Ein Kreis unter den Koordinaten (100, 100) mit einem Radius von 50 lässt sich also wie folgt zeichnen:
```typescript
// innerhalb der `draw` Funktion
canvas.drawCircle(new Vec2(100, 100), 50);
```

```typescript
// weitere Formen

// ein Rechteck mit einer Größe von 100x100 an der Position (100, 300)
canvas.drawRect(new Vec2(100, 300), new Vec2(100, 100));

// eine Linie von (100, 500) nach (200, 600)
canvas.drawLine(new Vec2(100, 500), new Vec2(200, 600));

// der Text "Hallo!" mit einer Schriftgröße von 25 unter (300, 100)
canvas.drawText("Hallo!", new Vec2(300, 100), { size: 25 });
```

Teste die Zeichenfunktionen am besten aus, um ein Gefühl für das Koordinatensystem zu bekommen.

