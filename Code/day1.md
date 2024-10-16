## MongoDB Installation

### Installation on Windows:
1. Download MongoDB from the official website.
2. Run the `.exe` file and follow the installation instructions.
3. Install the `mongosh` shell.

### Installation on macOS:
```bash
brew tap mongodb/brew
brew install mongodb-community@5.0
```

### Installation on Linux (Ubuntu):
```bash
sudo apt-get install -y mongodb-org
```

## Example JSON Document

```json
{
  "name": "MongoDB",
  "type": "database",
  "created_at": "2009-02-12T08:45:00Z",
  "is_open_source": true,
  "features": ["high_performance", "scalability", "flexible_schema"]
}
```

## BSON Representation

BSON (Binary JSON) is a binary encoding used by MongoDB to store documents.

### Example BSON (binary):
```bson
```

## Replica Set Configuration

### Example Configuration (mongod.conf)
```yaml
replication:
  replSetName: "rs0"
net:
  bindIp: 127.0.0.1
  port: 27017
```

### Initialize the Replica Set:
```bash
rs.initiate(
  {
    _id: "rs0",
    members: [
      { _id: 0, host: "localhost:27017" },
      { _id: 1, host: "localhost:27018" },
      { _id: 2, host: "localhost:27019" }
    ]
  }
)
```

## MongoDB Shell Commands

- List all databases:
```bash
show dbs
```

- Switch to a database:
```bash
use myDatabase
```

- Show all collections:
```bash
show collections
```

- Find documents:
```bash
db.myCollection.find()
```

## Basic CRUD Operations

### Create:
```bash
db.users.insertOne({ "name": "Alice", "email": "alice@example.com" })
```

### Read:
```bash
db.users.find({ "name": "Alice" })
```

### Update:
```bash
db.users.updateOne({ "name": "Alice" }, { $set: { "email": "alice@newdomain.com" } })
```

### Delete:
```bash
db.users.deleteOne({ "name": "Alice" })
```
