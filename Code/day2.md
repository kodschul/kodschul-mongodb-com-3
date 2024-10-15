## Creating a Simple Index

```bash
db.orders.createIndex({ "orderDate": 1 })
```

This index improves query efficiency when searching for orders by the `orderDate`.

## Creating a Composite Index

```bash
db.orders.createIndex({ "customerId": 1, "orderDate": -1 })
```

This index will optimize queries that sort by customer and date in descending order.

## CRUD Operations in MongoDB Shell

### Create Operation
```bash
db.customers.insertOne({ "name": "Jane Doe", "email": "jane@example.com", "age": 25 })
```

### Read Operation
```bash
db.customers.find({ "name": "Jane Doe" })
```

### Update Operation
```bash
db.customers.updateOne({ "name": "Jane Doe" }, { $set: { "email": "jane.doe@newmail.com" } })
```

### Delete Operation
```bash
db.customers.deleteOne({ "name": "Jane Doe" })
```

## Useful MongoDB Shell Commands

- List all databases:
```bash
show dbs
```

- Switch to a specific database:
```bash
use myDatabase
```

- Show all collections in the current database:
```bash
show collections
```

- Find documents in a collection:
```bash
db.myCollection.find()
```

## Automating MongoDB with Shell Scripting

Here is an example script to automate database backup using `mongodump`:

```bash
#!/bin/bash
BACKUP_DIR="/backups/$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"
mongodump --out "$BACKUP_DIR"
echo "Backup completed at $BACKUP_DIR"
```
