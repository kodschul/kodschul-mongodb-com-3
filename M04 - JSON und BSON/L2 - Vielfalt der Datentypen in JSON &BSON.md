## MongoDB für .NET Schulung: Datentypen und Verwendung in MongoDB

MongoDB verwendet JSON-ähnliche BSON-Dokumente (Binary JSON), um Daten zu speichern. Verstehen der verschiedenen Datentypen und ihrer Verwendung ist entscheidend, um effektiv mit MongoDB zu arbeiten. Diese Schulung bietet einen Überblick über die Datentypen in JSON/BSON und deren praktische Anwendung in MongoDB.

### Verschiedene Datentypen in JSON/BSON

MongoDB speichert Daten in BSON, einem binären Format von JSON. BSON unterstützt eine Vielzahl von Datentypen, die in JSON nicht standardmäßig vorhanden sind. Hier sind die wichtigsten Datentypen:

#### 1. **String**

- **Beschreibung**: Ein Zeichenfolgenwert, der in MongoDB als UTF-8 kodiert gespeichert wird.
- **BSON-Typ**: `string`
- **Beispiel**: `"name": "Alice"`

#### 2. **Integer**

- **Beschreibung**: Ganzzahlige Werte. MongoDB unterstützt verschiedene Integer-Typen, einschließlich 32-Bit und 64-Bit.
- **BSON-Typ**: `int32` (32-Bit) und `int64` (64-Bit)
- **Beispiel**: `"age": 30`

#### 3. **Double**

- **Beschreibung**: Fließkommazahl. Verwendet für präzise mathematische Berechnungen.
- **BSON-Typ**: `double`
- **Beispiel**: `"price": 19.99`

#### 4. **Boolean**

- **Beschreibung**: Ein Wahrheitswert, der entweder `true` oder `false` sein kann.
- **BSON-Typ**: `boolean`
- **Beispiel**: `"isActive": true`

#### 5. **Date**

- **Beschreibung**: Ein Datum- und Zeitwert. Speichert Zeitstempel mit Millisekunden-Genauigkeit.
- **BSON-Typ**: `date`
- **Beispiel**: `"createdAt": ISODate("2024-07-31T12:00:00Z")`

#### 6. **Array**

- **Beschreibung**: Eine Liste von Werten, die von verschiedenen Datentypen sein können.
- **BSON-Typ**: `array`
- **Beispiel**: `"tags": ["mongodb", "database", "NoSQL"]`

#### 7. **Object**

- **Beschreibung**: Ein verschachteltes Dokument, das zusätzliche Schlüssel-Wert-Paare enthält.
- **BSON-Typ**: `embedded document`
- **Beispiel**: `"address": { "street": "123 Main St", "city": "Anytown" }`

#### 8. **Null**

- **Beschreibung**: Ein Nullwert, der anzeigt, dass kein Wert vorhanden ist.
- **BSON-Typ**: `null`
- **Beispiel**: `"middleName": null`

#### 9. **Binary Data**

- **Beschreibung**: Binäre Daten wie Bilder oder Dateien.
- **BSON-Typ**: `binary`
- **Beispiel**: `"profilePicture": BinData(0, "binarydatahere")`

#### 10. **ObjectId**

- **Beschreibung**: Ein eindeutiger Identifikator, der automatisch von MongoDB generiert wird.
- **BSON-Typ**: `objectId`
- **Beispiel**: `_id: ObjectId("507f191e810c19729de860ea")`

### Praktische Beispiele und Anwendungsfälle in MongoDB

#### Beispiel 1: Benutzerprofil

In einem Benutzerprofil-Dokument können verschiedene Datentypen verwendet werden, um unterschiedliche Arten von Informationen zu speichern.

```json
{
  "_id": ObjectId("507f191e810c19729de860ea"),
  "name": "Alice",
  "age": 30,
  "email": "alice@example.com",
  "isActive": true,
  "createdAt": ISODate("2024-07-31T12:00:00Z"),
  "tags": ["mongodb", "database", "NoSQL"],
  "address": {
    "street": "123 Main St",
    "city": "Anytown"
  },
  "profilePicture": BinData(0, "binarydatahere")
}
```

#### Beispiel 2: Produktkatalog
In einem Produktkatalog-Dokument können Sie verschiedene Typen von Daten wie Preise, Verfügbarkeiten und Kategorien speichern.

```json
{
  "_id": ObjectId("507f191e810c19729de860eb"),
  "productName": "Laptop",
  "price": 999.99,
  "inStock": true,
  "categories": ["electronics", "computers"],
  "releaseDate": ISODate("2024-06-01T00:00:00Z")
}
```

#### Beispiel 3: Log-Dateien
Für Log-Dateien können Sie Zeitstempel, Log-Nachrichten und Statusinformationen speichern.

```json
{
  "_id": ObjectId("507f191e810c19729de860ec"),
  "timestamp": ISODate("2024-07-31T12:34:56Z"),
  "level": "error",
  "message": "Failed to connect to database",
  "details": {
    "errorCode": 500,
    "description": "Internal Server Error"
  }
}

```