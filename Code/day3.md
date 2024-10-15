# MongoDB Admins - Code Examples (Tag 3/3)

This document contains all the code examples extracted from the training slides (Tag 3/3). The examples are fully functional and compatible with the latest MongoDB version.


## Setting Up a Sharded Cluster

```bash
# Start MongoDB config servers
mongod --configsvr --replSet configReplSet --dbpath /data/configdb --port 27019

# Start MongoDB shard servers
mongod --shardsvr --replSet shardReplSet1 --dbpath /data/shard1 --port 27018
mongod --shardsvr --replSet shardReplSet2 --dbpath /data/shard2 --port 27017

# Start mongos query router
mongos --configdb configReplSet/localhost:27019 --port 27020
```

- Use a shard key to distribute data across shards:
```bash
db.myCollection.createIndex({ "shardKeyField": 1 })
sh.enableSharding("myDatabase")
sh.shardCollection("myDatabase.myCollection", { "shardKeyField": 1 })
```

## Backup and Restore Operations

### Backup with `mongodump`
```bash
mongodump --db myDatabase --out /backup/path
```

### Restore with `mongorestore`
```bash
mongorestore --db myDatabase /backup/path/myDatabase
```

## Import and Export Operations

### Importing Data with `mongoimport`
```bash
mongoimport --db myDatabase --collection myCollection --file data.json --jsonArray
```

### Exporting Data with `mongoexport`
```bash
mongoexport --db myDatabase --collection myCollection --out data.json --jsonArray
```

## Aggregation Framework

### Simple Aggregation Example
```bash
db.sales.aggregate([
  { $match: { status: "A" } },
  { $group: { _id: "$cust_id", totalAmount: { $sum: "$amount" } } }
])
```

### Using $lookup for Joins
```bash
db.customers.aggregate([
  { $lookup: {
      from: "orders",
      localField: "cust_id",
      foreignField: "customer_id",
      as: "order_docs"
    }
  }
])
```

## Geospatial Indexing

### Creating a 2dsphere Index for Geospatial Queries
```bash
db.places.createIndex({ location: "2dsphere" })
```

### Performing a Radius Query
```bash
db.places.find({
  location: {
    $geoWithin: {
      $centerSphere: [ [ -73.97, 40.77 ], 10 / 3963.2 ]  # 10 mile radius
    }
  }
})
```

## Object-Document Mapping (ODM)

### Defining a POCO Class in C#
```csharp
public class Customer
{
    public string Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

### Querying Data with MongoDB.Driver in C#
```csharp
var customers = await db.GetCollection<Customer>("customers")
    .Find(c => c.Name == "John Doe")
    .ToListAsync();
```
