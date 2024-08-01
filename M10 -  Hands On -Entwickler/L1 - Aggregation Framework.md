## MongoDB für .NET: Daten analysieren mit dem Aggregation Framework

MongoDB ist eine NoSQL-Datenbank, die das Aggregation Framework bereitstellt, um komplexe Datenanalysen und -transformationen durchzuführen. Dieses Framework ermöglicht es, Daten effizient zu aggregieren, zu filtern, zu gruppieren und zu transformieren. In einer .NET-Umgebung kann das Aggregation Framework über die MongoDB C#-Treiber verwendet werden. Im Folgenden werden die Grundprinzipien und wichtige Operationen des Aggregation Frameworks vorgestellt.

### Grundprinzipien des Aggregation Frameworks

Das Aggregation Framework besteht aus einer Pipeline von Stufen (Stages), durch die Dokumente nacheinander verarbeitet werden. Jede Stufe transformiert die Daten und gibt die Ergebnisse an die nächste Stufe weiter. Dies ermöglicht eine leistungsstarke und flexible Datenverarbeitung.

### Wichtige Aggregationsstufen

#### 1. `$match`

Die `$match`-Stufe filtert Dokumente basierend auf einer angegebenen Bedingung. Sie ist vergleichbar mit einer WHERE-Klausel in SQL.

- **Beispiel**: Filtern von Dokumenten, bei denen das Feld `status` den Wert `"active"` hat.

```csharp
var filter = Builders<BsonDocument>.Filter.Eq("status", "active");
var pipeline = new[] { new BsonDocument("$match", filter) };
```

### 2. $group
Die $group-Stufe gruppiert Dokumente basierend auf einem oder mehreren Feldern und ermöglicht Aggregationen wie Zählen, Summieren oder Mittelwertberechnungen.

Beispiel: Gruppieren von Dokumenten nach dem Feld category und Berechnung der Anzahl der Dokumente in jeder Kategorie.

```csharp
var groupStage = new BsonDocument("$group", new BsonDocument
{
    { "_id", "$category" },
    { "count", new BsonDocument("$sum", 1) }
});
var pipeline = new[] { groupStage };
```

### 3. $sort
Die $sort-Stufe sortiert Dokumente nach einem oder mehreren Feldern.

Beispiel: Sortieren von Dokumenten nach dem Feld date in absteigender Reihenfolge.

```csharp
var sortStage = new BsonDocument("$sort", new BsonDocument("date", -1));
var pipeline = new[] { sortStage };
```

### 4. $project
Die $project-Stufe transformiert Dokumente, indem sie Felder hinzufügt, entfernt oder umbenennt.

Beispiel: Behalten der Felder name und price und Umbenennen des Feldes price in cost.

```csharp
var projectStage = new BsonDocument("$project", new BsonDocument
{
    { "name", 1 },
    { "cost", "$price" }
});
var pipeline = new[] { projectStage };
```

### 5. $limit und $skip
Die $limit-Stufe begrenzt die Anzahl der zurückgegebenen Dokumente, während die $skip-Stufe eine bestimmte Anzahl von Dokumenten überspringt.

Beispiel: Begrenzen der Ergebnisse auf 10 Dokumente und Überspringen der ersten 5 Dokumente.

```csharp
var limitStage = new BsonDocument("$limit", 10);
var skipStage = new BsonDocument("$skip", 5);
var pipeline = new[] { skipStage, limitStage };
```