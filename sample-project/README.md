# MongoDB Sample Project

This sample uses the **CleanStart MongoDB** image (`cleanstart/mongodb:latest-dev`) to run a container and demonstrates adding, updating, and retrieving data.

## 1. Pull and run the container

```bash
docker pull cleanstart/mongodb:latest-dev
```

```bash
docker run -d \
  --name mongodb-demo \
  -p 27017:27017 \
  cleanstart/mongodb:latest-dev
```

## 2. Connect to the shell

```bash
docker exec -it mongodb-demo mongosh
```

## 3. Add data

In `mongosh`, switch to a database and insert documents:

```javascript
use demodb

// Insert one document
db.products.insertOne({
  name: "Widget",
  price: 9.99,
  quantity: 100
})

// Insert multiple documents
db.products.insertMany([
  { name: "Gadget", price: 19.99, quantity: 50 },
  { name: "Gizmo",  price: 4.99,  quantity: 200 }
])
```

## 4. Update data

```javascript
// Update one document (e.g. change price of "Widget")
db.products.updateOne(
  { name: "Widget" },
  { $set: { price: 12.99, updatedAt: new Date() } }
)

// Update multiple documents (e.g. add a field to all)
db.products.updateMany(
  {},
  { $set: { inStock: true } }
)
```

## 5. Retrieve data

```javascript
// Find all documents in the collection
db.products.find()

// Pretty-print
db.products.find().pretty()

// Find one document
db.products.findOne({ name: "Widget" })

// Find with a filter
db.products.find({ price: { $lt: 15 } })

// Count documents
db.products.countDocuments()
```

Type `exit` to leave `mongosh`.

## Clean up

```bash
docker stop mongodb-demo
docker rm mongodb-demo
```

## Resources

- [CleanStart](https://cleanstart.com/)
- [MongoDB Server Documentation](https://www.mongodb.com/docs/manual/)
