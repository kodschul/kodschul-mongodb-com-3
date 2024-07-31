## MongoDB für .NET Schulung: Single Instance

### Grundlagen der Single Instance

Eine Single Instance MongoDB-Installation bezieht sich auf die Konfiguration und den Betrieb einer einzelnen MongoDB-Datenbankinstanz auf einem Server. Diese Konfiguration ist die einfachste und schnellste Möglichkeit, MongoDB in Betrieb zu nehmen und eignet sich gut für Entwicklungsumgebungen, Tests und einfache Anwendungsfälle, bei denen hohe Verfügbarkeit und Skalierbarkeit nicht kritisch sind.

#### Merkmale einer Single Instance

- **Einfachheit**: Eine einzelne MongoDB-Instanz ist einfach zu installieren, zu konfigurieren und zu verwalten.
- **Single Point of Failure (SPOF)**: Da es nur eine Instanz gibt, ist die Datenbank nicht fehlertolerant und ein Ausfall des Servers führt zum Verlust des Datenzugriffs.
- **Eingeschränkte Skalierbarkeit**: Alle Daten und Anfragen werden von einem einzigen Server gehandhabt, was die Skalierbarkeit begrenzt.

#### Einsatzgebiete

- **Entwicklungs- und Testumgebungen**: Schnell einzurichten und ideal zum Testen von Anwendungen.
- **Kleine Anwendungen**: Geeignet für Anwendungen mit geringem Datenvolumen und wenigen gleichzeitigen Zugriffen.

### Vor- und Nachteile im Vergleich zu anderen Modellen

#### Vorteile

1. **Einfache Installation und Konfiguration**
   - Der Installationsprozess für eine einzelne MongoDB-Instanz ist unkompliziert und erfordert nur minimale Konfigurationsanpassungen.
   - Beispiel: Starten einer Instanz mit dem Befehl `mongod` und Standardkonfiguration.

2. **Geringe Kosten**
   - Keine Notwendigkeit für zusätzliche Hardware oder komplexe Netzwerkinfrastrukturen.
   - Ideal für kostengünstige Setups und Proof-of-Concept-Projekte.

3. **Einfaches Management**
   - Weniger Komponenten zu überwachen und zu verwalten.
   - Keine Replikations- oder Sharding-Konfiguration erforderlich.

#### Nachteile

1. **Single Point of Failure (SPOF)**
   - Ausfall der Instanz führt zum kompletten Datenverlust und Unterbrechung des Datenzugriffs.
   - Kein Failover-Mechanismus vorhanden.

2. **Begrenzte Skalierbarkeit**
   - Leistung und Kapazität sind auf die Ressourcen des einzelnen Servers beschränkt.
   - Kann bei hohen Lasten oder großen Datenmengen schnell an die Grenzen stoßen.

3. **Keine Hochverfügbarkeit**
   - Bei einem Serverausfall ist die Datenbank nicht verfügbar.
   - Keine automatische Datenwiederherstellung oder Redundanz.

### Beispiel: Installation und Betrieb einer Single Instance

#### Installation

**Windows**

1. **MongoDB Community Server herunterladen**: Von der offiziellen MongoDB-Website herunterladen und den MSI-Installer ausführen.
2. **Installation durchführen**: Den Anweisungen im Installationsassistenten folgen und die Standardoptionen wählen.
3. **MongoDB-Dienst starten**: Über die Diensteverwaltung (`services.msc`) den MongoDB-Dienst starten.

**Linux (Ubuntu)**

1. **Repository hinzufügen**:
    ```sh
    wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
    sudo apt-get update
    ```
2. **Installation**:
    ```sh
    sudo apt-get install -y mongodb-org
    ```
3. **MongoDB-Dienst starten**:
    ```sh
    sudo systemctl start mongod
    sudo systemctl enable mongod
    ```

#### Betrieb

1. **Konfiguration**: Die Konfigurationsdatei (`mongod.conf` auf Linux oder `mongod.cfg` auf Windows) anpassen, falls erforderlich (z.B. Datenverzeichnis, Port, Authentifizierung).
2. **Starten des MongoDB-Servers**:
    ```sh
    mongod --config /path/to/mongod.conf
    ```
3. **Verbindung herstellen**: Die MongoDB-Shell verwenden, um sich mit der Instanz zu verbinden und erste Befehle auszuführen:
    ```sh
    mongo
    ```

### Fazit

Eine Single Instance MongoDB-Konfiguration ist ideal für Entwicklungsumgebungen und kleine Anwendungen, bei denen Einfachheit und Kosteneffizienz im Vordergrund stehen. Für produktive Umgebungen mit Anforderungen an Hochverfügbarkeit und Skalierbarkeit sollte jedoch eine Replikatsets oder Sharding in Betracht gezogen werden.
