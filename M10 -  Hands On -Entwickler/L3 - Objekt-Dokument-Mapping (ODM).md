## MongoDB für .NET: Objekt-Dokument-Mapping (ODM)

Objekt-Dokument-Mapping (ODM) ist ein Konzept, das die Abbildung von Objekten in einer objektorientierten Programmiersprache auf Dokumente in einer dokumentenorientierten Datenbank wie MongoDB ermöglicht. In der .NET-Welt wird dieses Mapping durch spezielle Bibliotheken und Tools unterstützt, die die Interaktion mit MongoDB erleichtern.

### Was ist Objekt-Dokument-Mapping (ODM)?

ODM ist eine Technik, die es Entwicklern ermöglicht, mit Datenbankdokumenten auf eine Weise zu arbeiten, die mit den Prinzipien der objektorientierten Programmierung übereinstimmt. Es übersetzt zwischen der objektorientierten Welt (Klassen und Objekte) und der dokumentenorientierten Welt (Dokumente in einer NoSQL-Datenbank).

### Vorteile von ODM

1. **Abstraktion und Vereinfachung**: ODM abstrahiert die Details der Datenbankinteraktionen und ermöglicht es Entwicklern, sich auf die Geschäftslogik und Datenmodelle zu konzentrieren.
2. **Typensicherheit**: Durch die Verwendung von stark typisierten Klassen wird die Integrität der Datenstruktur gewährleistet und Typfehler zur Entwicklungszeit erkannt.
3. **Automatisierung**: ODM-Bibliotheken automatisieren viele der wiederkehrenden Aufgaben wie das Einfügen, Abrufen und Aktualisieren von Daten, was die Produktivität erhöht.

### MongoDB ODM für .NET

Für .NET-Entwickler gibt es mehrere ODM-Bibliotheken, aber die am weitesten verbreitete ist **MongoDB.Driver**. Diese Bibliothek bietet umfassende Funktionen zur Interaktion mit MongoDB und zur Abbildung von .NET-Klassen auf MongoDB-Dokumente.

#### Beispiel für die Verwendung von MongoDB.Driver

1. **Installation des MongoDB.Driver Pakets**

   Um MongoDB.Driver in einem .NET-Projekt zu verwenden, muss das Paket installiert werden. Dies kann über NuGet erfolgen:

   ```bash
   dotnet add package MongoDB.Driver
    ```

2. **Definition eines Datenmodells**

    Definieren Sie eine C#-Klasse, die die Struktur eines MongoDB-Dokuments repräsentiert. Jede Eigenschaft der Klasse entspricht einem Feld im Dokument.

    ```csharp
    using MongoDB.Bson;
    using MongoDB.Bson.Serialization.Attributes;

    public class Person
    {
        [BsonId]
        public ObjectId Id { get; set; }

        [BsonElement("name")]
        public string Name { get; set; }

        [BsonElement("age")]
        public int Age { get; set; }
    }

    ```

    In diesem Beispiel repräsentiert die Klasse Person ein Dokument in der MongoDB-Datenbank. Die BsonId-Annotation kennzeichnet das Id-Feld als Primärschlüssel, und die BsonElement-Annotationen spezifizieren die Namen der Felder in den MongoDB-Dokumenten.

3. **Verbindung zur MongoDB-Datenbank und CRUD-Operationen**

    Hier ist ein einfaches Beispiel, wie Sie mit MongoDB.Driver eine Verbindung zur Datenbank herstellen und CRUD-Operationen ausführen:

    ```csharp
        using MongoDB.Driver;
        using System;
        using System.Threading.Tasks;

        class Program
        {
            private static IMongoCollection<Person> GetCollection()
            {
                var client = new MongoClient("mongodb://localhost:27017");
                var database = client.GetDatabase("testdb");
                return database.GetCollection<Person>("people");
            }

            static async Task Main(string[] args)
            {
                var collection = GetCollection();

                // Erstellen eines neuen Dokuments
                var person = new Person { Name = "John Doe", Age = 30 };
                await collection.InsertOneAsync(person);

                // Abrufen eines Dokuments
                var retrievedPerson = await collection.Find(p => p.Name == "John Doe").FirstOrDefaultAsync();
                Console.WriteLine($"Name: {retrievedPerson.Name}, Age: {retrievedPerson.Age}");

                // Aktualisieren eines Dokuments
                var filter = Builders<Person>.Filter.Eq(p => p.Name, "John Doe");
                var update = Builders<Person>.Update.Set(p => p.Age, 31);
                await collection.UpdateOneAsync(filter, update);

                // Löschen eines Dokuments
                await collection.DeleteOneAsync(p => p.Name == "John Doe");
            }
        }

    ```

    In diesem Beispiel wird eine Verbindung zur MongoDB-Datenbank hergestellt, ein Dokument eingefügt, abgerufen, aktualisiert und schließlich gelöscht.