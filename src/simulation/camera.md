# Kamerasteuerung (Zoom)

Um in größeren Simulationen einen besseren überblick behalten zu können empfiehlt sich die Fähigkeit,
die Kamera bewegen und zoomen zu können.
Dies lässt sich durch 2 Plugins der Kamera realisieren:
```typescript
// ... let canvas = 
canvas.addPlugin(new CanvasInputManagerPlugin());
canvas.addPlugin(new CanvasDraggablePlugin());
// restliche Plugins
```

Nun sollte sich mit der Maus bewegen und mit dem Mausrad zoomen lassen.

