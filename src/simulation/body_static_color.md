# Statische Körper
Der Zentralkörper soll in den Meisten Fällen das Zentrum des Systems bleiben,
da die Simulation allerdings auf alle Körper angewannd wird sind Kleine Bewegungen
nicht zu vermeiden.
Um dieses Problem zu lösen kann dem Körper eine Eigenschaft `static` zugewiesen werden
welche die Krafteinwirkungen auf den eigenen Körper vollständig deaktiviert.
Dies kann wie folgt umgesetzt werden:
```typescript
class GravBody {
    // weiteres Feld der Klasse `GravBody`:
    isStatic: boolean;

    // Ergänzung des Konstruktors:
    constructor(/* Argumente */, isStatic: boolean = false) {
        this.isStatic = isStatic;
        // restlicher Konstruktor
    }

    update(body: GravBody) {
        // Abbruch der Aimulation falls der Körper statisch ist
        if(this.isStatic) { return; }
        
        // ... Rest der `update` Methode
    }
}

```

