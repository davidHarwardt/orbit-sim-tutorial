# Simulation von mehreren Körpern

Um mehrere Körper simulieren zu können benötigen wir eine Liste (Array) aus Körpern.
Das bedeutet wir wandeln die seperaten Deklarationen von `sun` und `earth` in eine Liste `bodies` um.
```typescript
// let sun = new GravBody(new Vec2(500, 500), new Vec2(0, 0), 1000);
// let earth = new GravBody(new Vec2(500, 300), new Vec2(1, 0), 20);

// umgewandelt zu =>

let bodies = [
    new GravBody(new Vec2(500, 500), new Vec2(0, 0), 1000), // sun
    new GravBody(new Vec2(500, 300), new Vec2(2, 0), 20),   // earth
];
```
In diese Liste können nun beliebig viele weitere Körper hinzugefügt werden.

Damit nun alle Körper der Liste geupdated werden muss die Liste in der `draw` Funktion
mit einer `for` Schleife durchlaufen werden. Das Durchlaufen ersetzt die einzelnen `draw` und `update` Aufrufe.
```typescript
// innerhalb der `draw` Funktion
// ...canvas.beginDraw();
for(let i = 0; i < bodies.length; i++) {
    bodies[i].draw(canvas);
    bodies[i].updateAll(bodies);
}
// ...canvas.endDraw();
```

Zuletzt muss noch die `updateAll` Methode der `GravBody` Klasse implementiert werden:
```typescript
updateAll(bodies: GravBody[]) {
    // durchlaufen aller Körper
    for(let i = 0; i < bodies.length; i++) {
        // Check ob anderer Körper unterschiedlich ist
        if(bodies[i] !== this) {
            // Aufruf der eigenen `update` mit dem anderen Körper
            this.update(bodies[i]);
        }
    }
}
```

