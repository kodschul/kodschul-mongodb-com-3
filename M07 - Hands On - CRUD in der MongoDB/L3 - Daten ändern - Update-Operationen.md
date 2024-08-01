## MongoDB für .NET: Daten ändern - Update-Operationen

In MongoDB sind Update-Operationen entscheidend, um Dokumente in einer Sammlung zu ändern. Diese Operationen ermöglichen es, Dokumente basierend auf verschiedenen Kriterien zu finden und die gewünschten Änderungen vorzunehmen. In .NET-Anwendungen werden MongoDB-Update-Operationen häufig durch die MongoDB C#-Treiberbibliothek durchgeführt. Im Folgenden werden die grundlegenden Update-Operationen und deren Anwendung in .NET vorgestellt.

### Grundlegende Update-Operationen

#### 1. Einfache Aktualisierung

Die einfachste Form der Aktualisierung besteht darin, ein einzelnes Dokument zu finden und es zu aktualisieren. Dies erfolgt durch die `UpdateOne`-Methode.

- **Methode**: `UpdateOne`
- **Beschreibung**: Aktualisiert das erste Dokument, das den Suchkriterien entspricht.

**Beispiel:**

```csharp
using MongoDB.Driver;

// Erstellen eines MongoClient-Objekts
var client = new MongoClient("mongodb://localhost:27017");
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

// Definieren des Filterkriteriums
var filter = Builders<BsonDocument>.Filter.Eq("name", "John Doe");

// Definieren der Update-Operation
var update = Builders<BsonDocument>.Update.Set("age", 30);

// Ausführen der UpdateOne-Operation
var result = collection.UpdateOne(filter, update);
```
In diesem Beispiel wird das Alter des Dokuments mit dem Namen "John Doe" auf 30 geändert.

#### 2. Mehrere Dokumente aktualisieren
Wenn mehrere Dokumente aktualisiert werden sollen, verwendet man die UpdateMany-Methode.

Methode: UpdateMany
Beschreibung: Aktualisiert alle Dokumente, die den Suchkriterien entsprechen.
Beispiel:


```csharp
using MongoDB.Driver;

// Erstellen eines MongoClient-Objekts
var client = new MongoClient("mongodb://localhost:27017");
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

// Definieren des Filterkriteriums
var filter = Builders<BsonDocument>.Filter.Eq("status", "inactive");

// Definieren der Update-Operation
var update = Builders<BsonDocument>.Update.Set("status", "active");

// Ausführen der UpdateMany-Operation
var result = collection.UpdateMany(filter, update);

```

In diesem Beispiel wird der Status aller Dokumente mit dem Status "inactive" auf "active" geändert.

#### 3. Nur das erste gefundene Dokument aktualisieren
Die FindOneAndUpdate-Methode findet ein Dokument und aktualisiert es in einem Schritt.

Methode: FindOneAndUpdate
Beschreibung: Findet ein Dokument, aktualisiert es und gibt das ursprüngliche oder das aktualisierte Dokument zurück.

```csharp
using MongoDB.Driver;

// Erstellen eines MongoClient-Objekts
var client = new MongoClient("mongodb://localhost:27017");
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

// Definieren des Filterkriteriums
var filter = Builders<BsonDocument>.Filter.Eq("name", "Jane Doe");

// Definieren der Update-Operation
var update = Builders<BsonDocument>.Update.Inc("age", 1);

// Ausführen der FindOneAndUpdate-Operation
var updatedDocument = collection.FindOneAndUpdate(filter, update);

```

In diesem Beispiel wird das Alter des Dokuments mit dem Namen "Jane Doe" um 1 erhöht, und das aktualisierte Dokument wird zurückgegeben.

### 4. Aktualisieren mit Bedingungen
Die Update-Methode erlaubt es, bedingte Updates durchzuführen, zum Beispiel mit Update-Operatoren wie $set, $unset, $inc usw.

Operatoren:
"$set": Setzt den Wert eines Feldes.
"$unset": Entfernt ein Feld.
"$inc": Erhöht den Wert eines numerischen Feldes.

```csharp
using MongoDB.Driver;

// Erstellen eines MongoClient-Objekts
var client = new MongoClient("mongodb://localhost:27017");
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

// Definieren des Filterkriteriums
var filter = Builders<BsonDocument>.Filter.Eq("name", "Alice");

// Definieren der Update-Operation
var update = Builders<BsonDocument>.Update
    .Set("status", "active")
    .Inc("age", 1);

// Ausführen der UpdateOne-Operation
var result = collection.UpdateOne(filter, update);

```

In diesem Beispiel wird der Status des Dokuments mit dem Namen "Alice" auf "active" gesetzt und das Alter um 1 erhöht.