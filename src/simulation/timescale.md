# Zeitskalierung

In der grundlegenden Implementation ist die Simulation an die Framerate (Bildwiederholungsrate, meistens 60fps) des Browsers gebunden,
has heißt wenn sich die Framerate ändert wird die Simulation schneller oder langsamer.
Um die Simulation von der Framerate unabhängig zu machen kann die gesamte Simulation um das Zeitdelta `dt` zwischen den Frames skaliert (multipliziert) werden.

```typescript
// in GravBody

// die `update` Methoden erhalten ein zusätzliches Argument `dt`
update(body: GravBody, dt: number) {
    // ...berechnung `acc`

    // die Werte von `acc` und `vel` werden entsprechend der Zeit skaliert
    // indem diese mit `dt` multipliziert werden
    this.vel = this.vel.add(acc.multS(dt));
    this.pos = this.pos.add(this.vel.multS(dt));
}

updateAll(bodies: GravBody[], dt: number) {
    // for...
        // `dt` wird an die einzelnen `update` Methoden weitergegeben
        this.update(bodies[i], dt);
    // ...
}
```
```typescript
// direkt in `main.ts` in der `draw` Funktion

// die `draw` Funktion erhält automatisch einen Wert für `dt`
// (in Millisekunden) als ersten Parameter
function draw(dt: number) {
    // ...

    // Umwandlung von `dt` in Sekunden
    let dtSeconds = dt / 1000;
    for(let i = 0; i < bodies.length; i++) {
        bodies[i].draw(canvas);
        bodies[i].updateAll(bodies, dtSeconds);
    }
}
```

Aufgrund der Skalierung kann die Bewegung der Körper langsamer oder schneller geworden sein.
Die Geschwindigkeit (der Geschwindigkeitsvektor) der Körper kann angepasst werden falls dies der Fall ist.

