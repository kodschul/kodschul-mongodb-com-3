## Erste Schritte mit der MongoDB Shell

Die MongoDB Shell ist ein interaktives Werkzeug, das verwendet wird, um mit MongoDB-Datenbanken zu interagieren. In dieser Schulung werden wir die grundlegenden Schritte durchgehen, um sich in der MongoDB Shell zurechtzufinden und grundlegende Operationen durchzuführen.

### 1. Verbindung zur MongoDB Shell herstellen

Um die MongoDB Shell zu verwenden, müssen Sie zunächst eine Verbindung zu Ihrem MongoDB-Server herstellen. Die Shell wird normalerweise über die Befehlszeile gestartet.

- **Befehl**: `mongo`
- **Verbindung zu einem spezifischen Server**: `mongo <hostname>:<port>`

Beispiel:
```bash
mongo localhost:27017
```

Dies stellt eine Verbindung zum MongoDB-Server auf Ihrem lokalen Rechner auf dem Standardport 27017 her.

### 2. Basisoperationen
### 2.1 Datenbanken anzeigen
Um alle verfügbaren Datenbanken anzuzeigen, verwenden Sie den Befehl show dbs:

```js
show dbs

```

Dieser Befehl listet alle Datenbanken auf, die auf dem MongoDB-Server vorhanden sind.

### 2.2 Eine Datenbank auswählen
Um mit einer bestimmten Datenbank zu arbeiten, verwenden Sie den Befehl use:

```js
use myDatabase

```

Dieser Befehl wählt die Datenbank myDatabase aus. Falls die Datenbank nicht existiert, wird sie erstellt, sobald Sie Daten in ihr speichern.

### 2.3 Eine Sammlung anzeigen
Innerhalb einer Datenbank können Sie die verfügbaren Sammlungen (Collections) anzeigen lassen:

```js
show collections

```

### 2.4 Dokumente einfügen
Um ein neues Dokument in eine Sammlung einzufügen, verwenden Sie die Methode insertOne oder insertMany:

```js
db.myCollection.insertOne({ name: "Alice", age: 30 })

```

Beispiel für mehrere Dokumente:

```js
db.myCollection.insertMany([
  { name: "Bob", age: 25 },
  { name: "Carol", age: 28 }
])

```

### 2.5 Dokumente abfragen
Um Dokumente aus einer Sammlung abzufragen, verwenden Sie die Methode find:

```js
db.myCollection.find()
```

Um die Ausgabe lesbarer zu machen, können Sie pretty() verwenden:

```js
db.myCollection.find().pretty()
```

### 2.6 Dokumente aktualisieren
Um Dokumente zu aktualisieren, verwenden Sie die Methode updateOne oder updateMany:

```js
db.myCollection.updateOne(
  { name: "Alice" },
  { $set: { age: 31 } }
)
```

### 2.7 Dokumente löschen
Um Dokumente zu löschen, verwenden Sie die Methode deleteOne oder deleteMany:

```js
db.myCollection.deleteOne({ name: "Alice" })
```

### 3. Arbeiten mit der MongoDB Shell in .NET
In .NET-Anwendungen können Sie die MongoDB-Datenbank über das MongoDB .NET Driver API verwalten. Hier sind einige grundlegende Schritte zur Verbindung und Interaktion mit MongoDB in .NET:

Installation des MongoDB .NET Drivers:

Fügen Sie den MongoDB .NET Driver zu Ihrem Projekt hinzu:

```bash
dotnet add package MongoDB.Driver
```

Verbindung zur MongoDB herstellen:

Beispielcode zum Herstellen einer Verbindung und Ausführen grundlegender Operationen:

```js
using MongoDB.Driver;

var client = new MongoClient("mongodb://localhost:27017");
var database = client.GetDatabase("myDatabase");
var collection = database.GetCollection<BsonDocument>("myCollection");

// Ein Dokument einfügen
var document = new BsonDocument { { "name", "Alice" }, { "age", 30 } };
collection.InsertOne(document);

// Dokumente abfragen
var documents = collection.Find(new BsonDocument()).ToList();

```