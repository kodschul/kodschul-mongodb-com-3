## MongoDB für .NET: Daten abfragen - Read-Operationen

MongoDB ist eine leistungsfähige NoSQL-Datenbank, die dokumentenorientiert ist und flexible Datenstrukturen bietet. In einer .NET-Anwendung können Sie die MongoDB C#-Treiber verwenden, um Daten abzufragen und Read-Operationen durchzuführen. Dieser Leitfaden gibt einen Überblick über die gängigen Read-Operationen in MongoDB und wie Sie diese mit .NET durchführen können.

### Grundlagen der Read-Operationen

MongoDB unterstützt verschiedene Arten von Read-Operationen, die es Ihnen ermöglichen, Daten aus Ihren Sammlungen zu lesen. Die grundlegenden Read-Operationen umfassen das Abrufen von Dokumenten, das Filtern von Ergebnissen und das Sortieren von Daten.

### 1. Verbindung zur MongoDB-Datenbank herstellen

Bevor Sie Daten abfragen können, müssen Sie eine Verbindung zu Ihrer MongoDB-Datenbank herstellen. Dies geschieht typischerweise über den `MongoClient`-Objekt.

```csharp
using MongoDB.Bson;
using MongoDB.Driver;

// Erstellen eines MongoClient-Objekts
var client = new MongoClient("mongodb://localhost:27017");

// Zugriff auf die Datenbank
var database = client.GetDatabase("mydatabase");

// Zugriff auf die Sammlung
var collection = database.GetCollection<BsonDocument>("mycollection");
```

### 2. Alle Dokumente abfragen
Um alle Dokumente aus einer Sammlung abzurufen, verwenden Sie die Methode Find ohne Filter.

```csharp
var allDocuments = collection.Find(new BsonDocument()).ToList();

// Ausgabe der Dokumente
foreach (var document in allDocuments)
{
    Console.WriteLine(document.ToJson());
}

```

### 3. Dokumente nach Kriterien filtern
Um Dokumente nach bestimmten Kriterien zu filtern, verwenden Sie Filter-Builder-Methoden. Hier ein Beispiel, wie Sie Dokumente mit einem bestimmten Feldwert abfragen.

```csharp
var filter = Builders<BsonDocument>.Filter.Eq("fieldname", "value");
var filteredDocuments = collection.Find(filter).ToList();

// Ausgabe der gefilterten Dokumente
foreach (var document in filteredDocuments)
{
    Console.WriteLine(document.ToJson());
}

```

### 4. Dokumente sortieren
Sie können Ergebnisse sortieren, indem Sie eine Sortierreihenfolge angeben. Hier ein Beispiel, wie Sie Dokumente nach einem bestimmten Feld sortieren.

```csharp
var sort = Builders<BsonDocument>.Sort.Ascending("fieldname");
var sortedDocuments = collection.Find(new BsonDocument()).Sort(sort).ToList();

// Ausgabe der sortierten Dokumente
foreach (var document in sortedDocuments)
{
    Console.WriteLine(document.ToJson());
}

```

### 5. Einzeldokumente abfragen
Um ein einzelnes Dokument basierend auf einem Filterkriterium abzurufen, verwenden Sie Find mit einer Einschränkung auf das erste gefundene Dokument.

```csharp
var singleDocument = collection.Find(filter).FirstOrDefault();

// Ausgabe des Dokuments
if (singleDocument != null)
{
    Console.WriteLine(singleDocument.ToJson());
}
else
{
    Console.WriteLine("Dokument nicht gefunden.");
}

```

### 6. Dokumente mit Projektion abfragen
Projektion ermöglicht es Ihnen, nur bestimmte Felder von Dokumenten abzurufen. Hier ein Beispiel, wie Sie nur bestimmte Felder zurückgeben.

```csharp
var projection = Builders<BsonDocument>.Projection.Include("fieldname");
var documentsWithProjection = collection.Find(new BsonDocument()).Project(projection).ToList();

// Ausgabe der projizierten Dokumente
foreach (var document in documentsWithProjection)
{
    Console.WriteLine(document.ToJson());
}

```