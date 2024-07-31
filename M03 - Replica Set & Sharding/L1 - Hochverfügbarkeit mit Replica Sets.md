# MongoDB für .NET: Einführung in Replica Sets

## Einführung in Replica Sets und deren Bedeutung

Replica Sets sind eine wesentliche Funktion von MongoDB, die hohe Verfügbarkeit und Redundanz für Ihre Datenbank gewährleistet. Ein Replica Set besteht aus mehreren MongoDB-Instanzen, die Daten replizieren, um Ausfallsicherheit und Datenintegrität sicherzustellen.

### Bedeutung von Replica Sets

- **Hohe Verfügbarkeit**: Im Falle eines Ausfalls einer Instanz übernimmt eine andere automatisch die Rolle des primären Knotens.
- **Datenredundanz**: Daten werden auf mehrere Knoten repliziert, was Datenverluste verhindert.
- **Leseskalierung**: Sekundäre Knoten können für Leseanfragen verwendet werden, um die Last auf den primären Knoten zu reduzieren.

## Wichtige Begriffe und Konzepte

- **Primary**: Der Knoten, der alle Schreiboperationen empfängt. Es gibt immer nur einen primären Knoten in einem Replica Set.
- **Secondary**: Knoten, die Daten vom primären Knoten replizieren. Diese Knoten können für Leseoperationen verwendet werden.
- **Arbiter**: Ein Knoten, der an der Wahl des primären Knotens teilnimmt, aber keine Daten repliziert. Ein Arbiter wird verwendet, um eine ungerade Anzahl von Knoten in einem Replica Set sicherzustellen.
- **Election**: Der Prozess, bei dem ein neuer primärer Knoten gewählt wird, wenn der aktuelle Primär ausfällt.

## Infrastruktur und Konfiguration

### Aufbau und Anforderungen an die Infrastruktur

Um ein Replica Set einzurichten, benötigen Sie mindestens drei MongoDB-Instanzen. Diese können auf physischen Servern, virtuellen Maschinen oder Container-basierten Umgebungen ausgeführt werden.

- **Minimum**: Drei Knoten (z. B. zwei sekundäre Knoten und ein Arbiter oder drei Replikationsknoten ohne Arbiter).
- **Empfohlen**: Eine ungerade Anzahl von Knoten, um sicherzustellen, dass immer eine Mehrheit erreicht werden kann.

### Schrittweise Konfiguration eines Replica Sets

#### Voraussetzungen

- Installierte MongoDB-Instanzen auf allen Knoten.
- Netzwerkverbindung zwischen den Knoten.

#### 1. MongoDB auf allen Knoten starten

Starten Sie MongoDB auf allen Knoten mit der Option, als Replica Set zu arbeiten.

```sh
mongod --replSet "rs0" --bind_ip localhost,<Knoten-IP>
```
#### 2. Verbindung zum Primärknoten herstellen
Verbinden Sie sich mit der MongoDB-Shell auf dem Knoten, den Sie als Primär initialisieren möchten.

```sh
mongo --host <Primärknoten-IP>
```

#### 3. Replica Set initialisieren
Initialisieren Sie das Replica Set mit dem folgenden Befehl:

```js
rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "<Primärknoten-IP>:27017" },
    { _id: 1, host: "<Sekundärknoten1-IP>:27017" },
    { _id: 2, host: "<Sekundärknoten2-IP>:27017" }
  ]
});
```

#### 4. Status des Replica Sets überprüfen
Überprüfen Sie den Status des Replica Sets, um sicherzustellen, dass alle Knoten korrekt hinzugefügt wurden:

```sh
rs.status();
```

#### 5. Konfiguration anpassen
Fügen Sie bei Bedarf zusätzliche Konfigurationsoptionen hinzu, wie z. B. Prioritäten für die Wahl des primären Knotens oder Verzögerungen bei der Replikation.

```sh
cfg = rs.conf();
cfg.members[1].priority = 0.5;
cfg.members[2].priority = 0.5;
rs.reconfig(cfg);
```

#### 6. Verbindungen in Ihrer .NET-Anwendung konfigurieren
Konfigurieren Sie Ihre .NET-Anwendung so, dass sie sich mit dem Replica Set verbindet. Dies erfolgt in der Regel durch Angabe der Verbindungszeichenfolge in der Konfigurationsdatei oder im Code.

```csharp
var connectionString = "mongodb://<Primärknoten-IP>:27017,<Sekundärknoten1-IP>:27017,<Sekundärknoten2-IP>:27017/?replicaSet=rs0";
var client = new MongoClient(connectionString);
var database = client.GetDatabase("your_database_name");
```