## https://mongoosejs.com/docs/guides.html
* Mongoose Core Concepts
    * Schemas
    * SchemaTypes
    * Connections
    * Models
    * Documents
    * Subdocuments
    * Queries
    * Validation
    * Middleware
    * Populate
    * Discriminators
    * Plugins
    * Faster Mongoose Queries With Lean
    * Query Casting
    * findOneAndUpdate
    * Getters and Setters
    * Virtuals
* Advanced Topics
    * Working with Dates
    * Custom Casting For Built-in Types
    * Custom SchemaTypes
* Integrations
    * Promises
    * AWS Lambda
    * Browser Library
    * GeoJSON
    * Transactions
    * MongoDB Driver Deprecation Warnings
    * Testing with Jest
    * SSL Connections



# Mongoose Core Concepts

### Schemas
* defining schema
```
const FooSchema = new Schema({
    date: { default: Date.now(), type: Date }, 
    power: [{ enable: Boolean, val: Number }], 
    role: { title: String, val: Number },
    title: String,
})
```
* creating
	* const Foo = mongoose.model('Foo', FooSchema)
* _id
    * 



### SchemaTypes
* type: Array, Boolean, Buffer, Date, Decimal128, Map, Mixed, Number, ObjectId, String,
### Connections
### Models
### Documents
### Subdocuments
### Queries
### Validation
### Middleware
### Populate
### Discriminators
### Plugins
### Faster Mongoose Queries With Lean
### Query Casting
### findOneAndUpdate
### Getters and Setters
### Virtuals