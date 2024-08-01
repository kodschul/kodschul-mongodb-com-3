## Geodaten in MongoDB nutzen

MongoDB bietet umfassende Unterstützung für geographische Daten und räumliche Abfragen durch seine Geospatial-Indexierung. Dies ermöglicht es Entwicklern, Ort- und Standortdaten effizient zu speichern, zu verarbeiten und abzufragen. In dieser Schulung werden die Grundlagen der Nutzung von Geodaten in MongoDB behandelt, einschließlich der Speicherung, Abfrage und Verarbeitung von räumlichen Informationen.

### Grundlegende Geodaten-Typen

MongoDB unterstützt verschiedene Geodaten-Typen, darunter:

- **Punkt (Point)**: Ein einzelner Ort im Raum, definiert durch Längen- und Breitengrad.
- **Linie (LineString)**: Eine Reihe von Punkten, die eine gerade Linie oder einen Pfad bilden.
- **Polygon**: Eine geschlossene Form, die durch eine Reihe von Punkten definiert wird und Flächen repräsentiert.

### Geodaten speichern

Um Geodaten in MongoDB zu speichern, verwenden Sie das GeoJSON-Format, das eine Standardmethode zur Darstellung geographischer Daten darstellt.

#### Beispiel: Speichern eines Punktes

```javascript
db.places.insertOne({
  name: "Central Park",
  location: {
    type: "Point",
    coordinates: [-73.968285, 40.785091] // [Längengrad, Breitengrad]
  }
});
```

In diesem Beispiel wird ein Ort ("Central Park") mit einem Punkt im GeoJSON-Format gespeichert.

### Geospatial-Indexierung
Um effiziente räumliche Abfragen durchzuführen, müssen Sie einen Geospatial-Index auf den Geodaten erstellen. MongoDB unterstützt verschiedene Arten von Geospatial-Indizes:

2dsphere Index: Unterstützt Abfragen auf geographischen Daten im GeoJSON-Format.
2d Index: Unterstützt Abfragen auf geographischen Daten im Kartesischen Koordinatensystem.
Beispiel: Erstellen eines 2dsphere-Indexes

```javascript
db.places.createIndex({ location: "2dsphere" });
```

```javascript
db.places.insertOne({
  name: "Central Park",
  location: {
    type: "Point",
    coordinates: [-73.968285, 40.785091] // [Längengrad, Breitengrad]
  }
});
```

Dieser Index ermöglicht schnelle räumliche Abfragen auf der location-Feld.

### Geospatial-Abfragen
MongoDB bietet verschiedene Abfragemethoden zur Verarbeitung und Analyse von Geodaten:

1. Nahegelegene Orte finden
Um Orte zu finden, die sich in der Nähe eines bestimmten Punktes befinden, verwenden Sie die $near-Operatoren.

```javascript
db.places.find({
  location: {
    $near: {
      $geometry: {
        type: "Point",
        coordinates: [-73.968285, 40.785091]
      },
      $maxDistance: 5000 // Entfernung in Metern
    }
  }
});

```

Dieser Abfrage findet Orte in einem Umkreis von 5 Kilometern um den angegebenen Punkt.

2. Orte innerhalb eines bestimmten Polygons finden
Um Orte zu finden, die sich innerhalb eines bestimmten Polygons befinden, verwenden Sie den $geoWithin-Operator.

```javascript
db.places.find({
  location: {
    $geoWithin: {
      $geometry: {
        type: "Polygon",
        coordinates: [[
          [-74, 40],
          [-74, 41],
          [-73, 41],
          [-73, 40],
          [-74, 40]
        ]]
      }
    }
  }
});

```

Diese Abfrage findet Orte innerhalb des angegebenen Polygons.

3. Entfernung zwischen zwei Punkten berechnen
Um die Entfernung zwischen zwei Punkten zu berechnen, verwenden Sie die $geoNear-Aggregation.


```javascript
db.places.aggregate([
  {
    $geoNear: {
      near: {
        type: "Point",
        coordinates: [-73.968285, 40.785091]
      },
      distanceField: "distance",
      spherical: true
    }
  }
]);

```

Diese Aggregation berechnet die Entfernung zwischen dem gegebenen Punkt und den gespeicherten Orten.