## MongoDB: Datenmodell

MongoDB ist eine NoSQL-Datenbank, die dokumentenorientiert arbeitet. Das Datenmodell von MongoDB besteht aus Dokumenten, die in Sammlungen (Collections) und Datenbanken organisiert sind. Dieses Modell bietet Flexibilität und Skalierbarkeit, die sich gut für eine Vielzahl von Anwendungen eignen. Im Folgenden werden die Struktur und die Eigenschaften von dokumentbasierten Datenmodellen in MongoDB beschrieben.

### Dokumente

Dokumente sind die Grundeinheit der Daten in MongoDB und werden im BSON-Format (Binary JSON) gespeichert. Jedes Dokument besteht aus einer Reihe von Schlüssel-Wert-Paaren, ähnlich wie ein JSON-Objekt. Dokumente können verschachtelte Strukturen enthalten und unterschiedliche Schemata haben, auch innerhalb derselben Sammlung.

#### Beispiel-Dokument

```json
{
  "_id": "507f1f77bcf86cd799439011",
  "name": "Alice",
  "age": 29,
  "address": {
    "street": "123 Main St",
    "city": "Metropolis",
    "zip": "12345"
  },
  "hobbies": ["reading", "hiking", "coding"]
}
```

_id: Ein eindeutiger Bezeichner für das Dokument. MongoDB generiert diesen Wert automatisch, falls er nicht angegeben wird.
name, age: Einfache Schlüssel-Wert-Paare.
address: Ein verschachteltes Dokument.
hobbies: Ein Array von Werten.
### Collections
Collections sind Gruppierungen von Dokumenten in MongoDB. Eine Collection entspricht in etwa einer Tabelle in relationalen Datenbanken, aber ohne ein festes Schema. Alle Dokumente innerhalb einer Collection können unterschiedliche Strukturen haben, was eine große Flexibilität bietet.

#### Eigenschaften von Collections
Schemasfreiheit: Dokumente innerhalb einer Collection können unterschiedliche Felder und Datentypen haben.
Indizes: Collections können Indizes auf beliebigen Feldern enthalten, um die Abfrageleistung zu verbessern.
Aggregation: MongoDB bietet leistungsstarke Aggregations-Frameworks, um komplexe Datenanalysen durchzuführen.
### Datenbanken
Datenbanken sind Container für Collections. Eine MongoDB-Instanz kann mehrere Datenbanken enthalten, die voneinander isoliert sind. Jede Datenbank hat ihre eigenen Sammlungen und Dokumente.

#### Beispiel für die Datenbankstruktur
Datenbank: myDatabase
##### Collection: users
Dokumente: Mehrere Dokumente mit Benutzerdaten
##### Collection: orders
Dokumente: Mehrere Dokumente mit Bestelldaten
### Struktur und Eigenschaften von Dokument-basierten Datenmodellen
#### Flexibilität
Schemafreiheit: Dokumente in einer Collection müssen nicht das gleiche Schema haben. Dies ermöglicht eine flexible und dynamische Datenmodellierung.
Verschachtelung: Dokumente können verschachtelte Dokumente und Arrays enthalten, was komplexe Datenstrukturen ermöglicht.
#### Effizienz
Einbettung: Daten, die häufig zusammen abgefragt werden, können in einem einzigen Dokument eingebettet werden. Dies reduziert die Anzahl der Joins und erhöht die Abfragegeschwindigkeit.
Indizes: MongoDB unterstützt Indizes auf Dokumentfeldern, einschließlich verschachtelter Felder und Arrays, um die Leistung zu optimieren.
#### Skalierbarkeit
Horizontale Skalierung: MongoDB unterstützt Sharding, eine Methode zur Verteilung von Daten über mehrere Maschinen, um mit wachsendem Datenvolumen und Abfrageanforderungen Schritt zu halten.
Replikation: MongoDB bietet automatische Replikation und Failover, um hohe Verfügbarkeit und Datensicherheit zu gewährleisten.