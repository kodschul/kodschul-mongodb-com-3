## MongoDB für .NET: Daten einfügen – Create-Operationen

MongoDB ist eine dokumentenorientierte NoSQL-Datenbank, die in .NET-Anwendungen häufig verwendet wird. Die grundlegende Operation zum Hinzufügen von Daten in MongoDB ist die Create-Operation. Diese Operation wird verwendet, um neue Dokumente in eine Sammlung einzufügen. Im Folgenden werden die grundlegenden Methoden und Konzepte für das Einfügen von Daten in MongoDB mit .NET beschrieben.

### Voraussetzungen

Um MongoDB in einer .NET-Anwendung zu verwenden, benötigen Sie die MongoDB.Driver-Bibliothek. Diese kann über NuGet in Ihr .NET-Projekt integriert werden.

```bash
dotnet add package MongoDB.Driver
```

### 1. Verbindung zur MongoDB-Datenbank herstellen
Bevor Sie Daten einfügen können, müssen Sie eine Verbindung zur MongoDB-Datenbank herstellen und eine Sammlung auswählen.

```csharp
using MongoDB.Driver;

var connectionString = "mongodb://localhost:27017";
var client = new MongoClient(connectionString);
var database = client.GetDatabase("mydatabase");
var collection = database.GetCollection<BsonDocument>("mycollection");

```

### 2. Einfache Create-Operation: Ein einzelnes Dokument einfügen
Um ein einzelnes Dokument in die Sammlung einzufügen, verwenden Sie die Methode InsertOne().

```csharp
using MongoDB.Bson;
using MongoDB.Driver;

var document = new BsonDocument
{
    { "Name", "Alice" },
    { "Age", 30 },
    { "City", "New York" }
};

collection.InsertOne(document);

```

In diesem Beispiel wird ein Dokument mit den Feldern "Name", "Age" und "City" in die Sammlung eingefügt.

### 3. Mehrere Dokumente einfügen
Um mehrere Dokumente gleichzeitig einzufügen, verwenden Sie die Methode InsertMany().

```csharp
using MongoDB.Bson;
using MongoDB.Driver;

var documents = new List<BsonDocument>
{
    new BsonDocument { { "Name", "Bob" }, { "Age", 25 }, { "City", "Los Angeles" } },
    new BsonDocument { { "Name", "Charlie" }, { "Age", 35 }, { "City", "Chicago" } }
};

collection.InsertMany(documents);

```

In diesem Beispiel werden zwei Dokumente auf einmal in die Sammlung eingefügt.

### 4. Daten einfügen mit einem Typisierten Modell
Statt rohen BSON-Dokumenten können Sie auch ein typisiertes Modell verwenden, um Daten einzufügen.

```csharp
using MongoDB.Bson.Serialization.Attributes;

public class Person
{
    [BsonId]
    public ObjectId Id { get; set; }

    public string Name { get; set; }
    public int Age { get; set; }
    public string City { get; set; }
}

var person = new Person
{
    Name = "David",
    Age = 40,
    City = "San Francisco"
};

collection.InsertOne(person);

```

In diesem Beispiel wird ein Dokument als Instanz der Klasse Person erstellt und in die Sammlung eingefügt.

### 5. Fehlerbehandlung bei Create-Operationen
Es ist wichtig, Fehler zu behandeln, die beim Einfügen von Dokumenten auftreten können, insbesondere wenn Sie mit größeren Datenmengen oder in produktiven Umgebungen arbeiten.

```csharp
try
{
    collection.InsertOne(document);
}
catch (MongoWriteException ex)
{
    // Fehlerbehandlung
    Console.WriteLine($"Fehler beim Einfügen des Dokuments: {ex.Message}");
}

```