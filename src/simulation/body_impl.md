# Implementation des Körpers

## Grundlegendes Prinzip
Da die Geschwindigkeit \\(v\\) eines Körpers die Änderung in seiner Position \\(p\\) beschreibt
und dasselbe für die Beschleunigung \\(a\\) und \\(v\\) gilt (\\(a\\) beschreibt die Änderungsrate von \\(v\\)),
wird in der Simulation jeden Frame in der `update` Methode eine Beschleunigung auf die Geschwindigkeit des Körpers addiert,
die Geschwindigkeit wiederum wird auf die Position addiert:

```typescript
// in der `GravBody` Klasse
update(body: GravBody) {
    // vorerst keine Beschleunigung
    let acc = /* ? */ new Vec2(0, 0);

    // in Javascript lassen sich nur Zahlen (number) mit dem `+` Operator addieren
    // daher verwenden Vektoren eine `add` Methode wie hier dargestellt
    // die restlichen Operationen können mit `sub`, `mult`, `div` verwendet werden
    this.vel = this.vel.add(acc);
    this.pos = this.pos.add(this.vel);
}
// ...
```

## Zeichnen des Körpers
Um den Körper anzeigen zu können, wird er in der `draw` Methode gezeichnet.
Für die Darstellung kann eine beliebige Form gewählt werden, allerdings entspricht ein Kreis den zu simulierenden Objekten am ehesten:
```typescript
// in der `GravBody` Klasse
draw(canvas: Canvas2d) {
    // grobe Abschätzung des Radius anhand der Masse
    let radius = Math.sqrt(this.mass);
    canvas.drawCircle(this.pos, radius);
}
```

## Darstellen der Körper
Mit dem grundlegenden Gerüst lassen sich die Körper bereits auf dem Bildschirm anzeigen und können sich _gleichförmig_ bewegen.
Um beispielhaft 2 Körper in der Simulation zu verwenden, kann die Simulation um das Folgende erweitert werden:
```typescript
// direkt in `main.ts`
// unter Code zum Erzeugen der Canvas
let sun = new GravBody(new Vec2(500, 500), new Vec2(0, 0), 1000);
let earth = new GravBody(new Vec2(500, 300), new Vec2(1, 0), 20);

function draw() {
    // ...canvas.beginDraw();
    earth.update(sonne);

    earth.draw(canvas);
    sun.draw(canvas);
    canvas.endDraw();
    // ... canvas.endDraw();
}
```
Wenn die Datei nun gespeichert wird, sollten ein großer und ein kleinerer Kreis, welcher sich nach rechts bewegt, auf dem Bildschirm zu erkennen sein.
Der kleine Kreis bewegt sich noch geradeaus, da sein Geschwindigkeitsvektor gleich bleibt und nach rechts zeigt.

## Implementation des Gravitationsgesetzes
Um die Position und Geschwindigkeit des Körpers simulieren zu können, muss also vorerst die, aus der Kraft resultierende Beschleunigung,
unter Verwendung der folgenden Formeln berechnet werden.
(die Formeln müssen nach \\(a\\) umgestellt werden und \\(G = \gamma\\))

\\[ F = G \frac{m_1 m_2}{r^2} \\]
\\[ F = m \cdot a \\]

<details>
<summary>Lösung</summary>

\\[ F = m_1 \cdot a \\]
Teilen durch \\(m\\)

\\[ a = \frac{F}{m_1} \\]
Einsetzen von \\(F\\)

\\[ a = \frac{G \frac{m_1 m_2}{r^2}}{m_1} \\]
Kürzen

\\[ a = G \frac{m_1 m_2}{m_1 r^2} \\]
\\[ \underline{\underline{a = G \frac{m_2}{r^2}}} \\]
</details>

Die Gleichung kann wie folgt in Javascript implementiert werden:
```typescript
update(body: GravBody) {
    // Gravitationskonstante (fiktiver Wert)
    let G = 1;
    // Berechnen der Entfernung zwischen den Körpern
    let r = this.pos.distance(body.pos);

    // Richtung der Beschleunigung
    // (Vektor, welcher in Richtung des anderen Körpers zeigt)
    // 
    // +-------------------->
    // |  this    other
    // |    x------>x
    // |       dir
    // |       
    // V
    let dir = body.pos.sub(this.pos);

    // Betrag der Beschleunigung (ohne Richtung)
    let absAcc = G * (body.mass / (r*r));
    // kombinieren von Richtung und Betrag der Beschleunigung
    let acc = dir.withLength(absAcc);

    this.vel = this.vel.add(acc);
    this.pos = this.pos.add(this.vel);
}
```
Wenn die Gleichung korrekt implementiert wurde, sollte die Erde in der Simulation um die Sonne kreisen.

Alle weitern Schritte dienen der Erweiterung der, nun fertigen, Grundsimulation

