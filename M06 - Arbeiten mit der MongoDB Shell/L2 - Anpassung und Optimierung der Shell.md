## MongoDB für .NET: Anpassung und Optimierung der Shell

MongoDB ist eine populäre NoSQL-Datenbank, die eine flexible Schema-Struktur und leistungsfähige Abfragefunktionen bietet. Die MongoDB-Shell (`mongo`) ist ein mächtiges Werkzeug zur Interaktion mit der Datenbank. In dieser Schulung werden wir uns mit der Anpassung und Optimierung der MongoDB-Shell beschäftigen, um die Effizienz und Benutzerfreundlichkeit zu verbessern.

### Anpassung der MongoDB-Shell

#### 1. Verwendung von Konfigurationsdateien

MongoDB ermöglicht die Verwendung von Konfigurationsdateien, um die Shell-Umgebung anzupassen. Diese Dateien können zum Beispiel benutzerdefinierte Funktionen oder Variablen enthalten, die bei jedem Start der Shell geladen werden.

- **Beispiel**: Eine Konfigurationsdatei `mongo_config.js` könnte benutzerdefinierte Funktionen definieren.

```javascript
// mongo_config.js
function log(msg) {
  print('Log: ' + msg);
}

db.customCollection = db.getCollection('myCollection');
```

Um diese Konfiguration zu laden, starten Sie die Shell mit:


```sh
mongo --eval "load('mongo_config.js')"
```

### 2. Verwendung von Shell-Skripten
Shell-Skripte sind eine hervorragende Möglichkeit, wiederkehrende Aufgaben zu automatisieren. Sie können Skripte erstellen, die mehrere MongoDB-Befehle enthalten, um komplexe Abläufe zu vereinfachen.

Beispiel: Ein Skript setup.js zum Erstellen von Indizes und initialen Daten.


```javascript
// setup.js
db.myCollection.createIndex({ name: 1 });
db.myCollection.insertMany([
  { name: 'Alice', age: 30 },
  { name: 'Bob', age: 25 }
]);

```

Führen Sie das Skript in der Shell aus:

```sh
mongo setup.js
```

### Optimierung der MongoDB-Shell
1. Verwendung von Aggregations-Pipelines
Die Aggregations-Pipeline in MongoDB ermöglicht komplexe Datenanalysen und -transformationen. Durch die Nutzung der Pipeline können Sie rechenintensive Operationen auf der Datenbankseite ausführen, um die Leistung der Anwendung zu verbessern.

Beispiel: Eine Aggregations-Pipeline zur Berechnung des Durchschnittsalters.

```javascript
db.myCollection.aggregate([
  { $group: { _id: null, averageAge: { $avg: "$age" } } }
]);

```

### 2. Indexierung zur Leistungssteigerung
Indexes sind entscheidend für die Optimierung von Abfragen in MongoDB. Durch das Erstellen geeigneter Indizes können Sie die Leistung der Abfragen erheblich verbessern.

Beispiel: Erstellen eines Indexes auf dem name-Feld.

```javascript
db.myCollection.createIndex({ name: 1 });
```

Überprüfen Sie die verwendeten Indizes mit:

```javascript
db.myCollection.getIndexes();
```

### 3. Nutzung von Profiling-Tools
MongoDB bietet Profiling-Tools, um langsame Abfragen zu identifizieren und zu optimieren. Der Profiler kann verwendet werden, um ausführliche Informationen zu den durchgeführten Abfragen zu erhalten.

Beispiel: Aktivieren des Profiler-Levels auf 1 (aufzeichnung aller langsamen Abfragen).

```javascript
db.setProfilingLevel(1, 100); // Profiling für Abfragen, die länger als 100ms dauern

```

Abfragen der Profiling-Daten:

```javascript
db.system.profile.find().pretty();

```