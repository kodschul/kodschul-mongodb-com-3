## MongoDB für .NET: Daten löschen - Delete-Operationen

In MongoDB können Daten auf verschiedene Weisen gelöscht werden. Diese Operationen sind wichtig, um nicht mehr benötigte oder veraltete Daten aus Ihrer Datenbank zu entfernen. Im Folgenden werden die verschiedenen Methoden zum Löschen von Daten in MongoDB beschrieben und wie diese in einer .NET-Anwendung verwendet werden können.

### Grundlegende Delete-Operationen in MongoDB

MongoDB bietet mehrere Methoden zum Löschen von Dokumenten in einer Sammlung. Die Hauptmethoden sind:

#### 1. `DeleteOne`

Die Methode `DeleteOne` wird verwendet, um ein einzelnes Dokument zu löschen, das der angegebenen Filterbedingung entspricht. Wenn mehrere Dokumente die Bedingung erfüllen, wird nur das erste gefundene Dokument gelöscht.

- **Syntax**: `DeleteOne(FilterDefinition<T> filter)`

- **Beispiel**: Löschen eines Dokuments, dessen `name`-Feld den Wert "John Doe" hat.

```csharp
using MongoDB.Driver;

// Erstellen Sie eine Instanz des MongoClient
var client = new MongoClient("mongodb://localhost:27017");

// Wählen Sie die Datenbank und die Sammlung aus
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

// Erstellen Sie einen Filter
var filter = Builders<BsonDocument>.Filter.Eq("name", "John Doe");

// Löschen eines Dokuments
var result = collection.DeleteOne(filter);
Console.WriteLine($"Anzahl der gelöschten Dokumente: {result.DeletedCount}");
```

### 2. DeleteMany
Die Methode DeleteMany wird verwendet, um alle Dokumente zu löschen, die der angegebenen Filterbedingung entsprechen. Diese Methode löscht möglicherweise mehrere Dokumente.

Syntax: DeleteMany(FilterDefinition<T> filter)

Beispiel: Löschen aller Dokumente, deren status-Feld den Wert "inactive" hat.

```csharp
using MongoDB.Driver;

// Erstellen Sie eine Instanz des MongoClient
var client = new MongoClient("mongodb://localhost:27017");

// Wählen Sie die Datenbank und die Sammlung aus
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

// Erstellen Sie einen Filter
var filter = Builders<BsonDocument>.Filter.Eq("status", "inactive");

// Löschen mehrerer Dokumente
var result = collection.DeleteMany(filter);
Console.WriteLine($"Anzahl der gelöschten Dokumente: {result.DeletedCount}");

```

### Wichtige Überlegungen
Filterkriterien: Die Filterkriterien bestimmen, welche Dokumente gelöscht werden. Seien Sie vorsichtig mit den Filterbedingungen, um unbeabsichtigtes Löschen zu vermeiden.

Transaktionen: In MongoDB können Sie Transaktionen verwenden, um sicherzustellen, dass mehrere Delete-Operationen atomar ausgeführt werden. Dies ist besonders wichtig, wenn Sie sicherstellen möchten, dass alle Löschvorgänge entweder vollständig abgeschlossen oder gar nicht durchgeführt werden.

Indexierung: Stellen Sie sicher, dass die Felder, die in den Filterkriterien verwendet werden, indiziert sind, um die Leistung der Löschoperationen zu verbessern.