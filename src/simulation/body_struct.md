# Struktur des Körpers

Um einen Körper simulieren zu können, benötigt dieser alle, für die Simulation wichtigen Daten.
Eine [Klasse](/sum.html#7-klassen) (`class`) eignet sich, um diese Eigenschaften zu lagern.

Die Klasse benötigt auch Methoden, welche den Körper zeichnen [`draw(canvas: Canvas2d)`]
und die Position und Geschwindigkeit nach dem Newtonschen Gravitationsgesetz
mit jeweils einem anderen Körper ändern [`update(body: GravBody)`].

Eine weitere Methode sollte die `update` Methode für alle Körper in der Simulation ausführen [`updateAll(bodies: GravBody[])`].

Beispielklasse:
```typescript
class GravBody {
    pos: Vec2;      // kurz für `position`
    vel: Vec2;      // kurz für `velocity`
    mass: number;

    constructor(pos: Vec2, vel: Vec2, mass: number) {
        this.pos = pos;
        this.vel = vel;
        this.mass = mass;
    }

    draw(canvas: Canvas2d) {
        // todo: Körper zeichnen
    }

    update(body: GravBody) {
        // todo: einzelnen Körper simulieren
    }

    updateAll(bodies: GravBody[]) {
        // todo: update für alle Körper (außer dem eigenen) aufrufen
    }
}
```

