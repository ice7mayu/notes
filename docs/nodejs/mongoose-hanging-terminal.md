# Mongoose

[Simple mongoose and node js Example](https://kb.objectrocket.com/mongo-db/simple-mongoose-and-node-js-example-1007)

## Hanging Terminal

The node.js program won't exit as long as a database connection is still open, so you need to close your connection pool after you're done with it like this:

```js
import mongoose from "mongoose";

mongoose.connect("mongodb://localhost:27017/dummy", {
    useNewUrlParser: true,
    useUnifiedTopology: true,
});

// Define a Schema
const kittySchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
    },
});

// Compile the Schema into a Model
const Kitten = mongoose.model("kittens", kittySchema);

const db = mongoose.connection;
db.on("error", console.error.bind(console, "connection error:"));
db.once("open", function () {
    console.log("connected to mongodb...");

    // Create a document(instance) from the Model
    const silence = new Kitten({ name: "Fluffy" });

    silence.save(function (err, newKitten) {
        if (err) return console.error(err);
        console.log(`Inserted a new kitten: ${newKitten.name}`);

        // To terminate the mongodb connection to make console exit gracefully
        mongoose.disconnect();
    });
});
```
