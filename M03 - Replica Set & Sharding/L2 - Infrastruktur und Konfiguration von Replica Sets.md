## MongoDB für .NET Schulung: Hands-On: Installation eines Replica Sets

### Praktische Übung zur Einrichtung eines Replica Sets

Ein Replica Set in MongoDB bietet Hochverfügbarkeit und Redundanz durch das Replizieren von Daten auf mehrere Knoten. In dieser praktischen Übung werden wir Schritt für Schritt ein Replica Set einrichten und konfigurieren.

#### Schritt-für-Schritt-Anleitung

**Voraussetzungen**:
- Drei oder mehr Server oder virtuelle Maschinen (VMs) für die MongoDB-Instanzen.
- MongoDB installiert auf allen beteiligten Servern.
- Netzwerkzugriff zwischen den Servern.

#### 1. Konfiguration der MongoDB-Instanzen

Auf jedem Server müssen Sie die MongoDB-Instanz so konfigurieren, dass sie Teil eines Replica Sets wird. Bearbeiten Sie die `mongod.conf`-Datei (standardmäßig unter `/etc/mongod.conf` auf Linux oder im Installationsverzeichnis auf Windows) und fügen Sie die folgenden Konfigurationen hinzu:

```yaml
replication:
  replSetName: "rs0"
```

#### 2. Starten der MongoDB-Instanzen
Starten Sie jede MongoDB-Instanz mit der aktualisierten Konfiguration:

Linux:
```sh
sudo systemctl restart mongod
```

Windows:
```sh
net stop MongoDB
net start MongoDB
```

#### 3. Initialisieren des Replica Sets
Melden Sie sich bei einer der MongoDB-Instanzen an und initialisieren Sie das Replica Set. Öffnen Sie die MongoDB-Shell (mongo) und führen Sie die folgenden Befehle aus:

```js
// Verbinden mit der primären Instanz
rs.initiate(
  {
    _id: "rs0",
    members: [
      { _id: 0, host: "server1:27017" },
      { _id: 1, host: "server2:27017" },
      { _id: 2, host: "server3:27017" }
    ]
  }
);
```
Ersetzen Sie server1, server2 und server3 durch die tatsächlichen Hostnamen oder IP-Adressen der Server.

#### 4. Überprüfen der Replikation
Überprüfen Sie den Status des Replica Sets, um sicherzustellen, dass alle Mitglieder korrekt konfiguriert und betriebsbereit sind:

```js
rs.status();
```


```yaml
replication:
  replSetName: "rs0"
```