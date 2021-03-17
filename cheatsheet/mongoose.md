## Mongoose Cheatsheet

```js
// IMPORT DEPENDENCIES
const {Schema, model} = require("mongoose")
/////////////////////////
// Create the Schema
////////////////////////
const schema = new Schema({
  name:    String,
  binary:  Buffer,
  living:  Boolean,
  updated: { type: Date, default: Date.now },
  age:     { type: Number, min: 18, max: 65 },
  mixed:   Schema.Types.Mixed,
  _someId: Schema.Types.ObjectId,
  decimal: Schema.Types.Decimal128,
  array: [],
  ofString: [String],
  ofNumber: [Number],
  ofDates: [Date],
  ofBuffer: [Buffer],
  ofBoolean: [Boolean],
  ofMixed: [Schema.Types.Mixed],
  ofObjectId: [Schema.Types.ObjectId],
  ofArrays: [[]],
  ofArrayOfNumbers: [[Number]],
  nested: {
    stuff: { type: String, lowercase: true, trim: true }
  },
  map: Map,
  mapOfString: {
    type: Map,
    of: String
  }
})
/////////////////////////
// Create the Model
////////////////////////
const Thing = model('Thing', schema);
/////////////////////////
// EXPORT THE MODEL
////////////////////////
module.exports = Thing
```

## Schema Options

```
required: boolean or function, if true adds a required validator for this property

default: Any or function, sets a default value for the path. If the value is a function, the return value of the function is used as the default.

select: boolean, specifies default projections for queries

validate: function, adds a validator function for this property

get: function, defines a custom getter for this property using Object.defineProperty().

set: function, defines a custom setter for this property using Object.defineProperty().

alias: string, mongoose >= 4.10.0 only. Defines a virtual with the given name that gets/sets this path.

immutable: boolean, defines path as immutable. Mongoose prevents you from changing immutable paths unless the parent document has isNew: true.

transform: function, Mongoose calls this function when you call Document#toJSON() function, including when you JSON.stringify() a document.
```

## Model Methods

- [Mongoose Model Methods](https://mongoosejs.com/docs/api/model.html)

## Query Helpers

- [Mongo Query Operators](https://docs.mongodb.com/manual/reference/operator/query/)

## Relationships

##### One to One Relationship

In a one to one relationship both models would include the key of the other.

## Example

```js
const { Schema, model } = require("mongoose")

//***********************
// CREATE THE SCHEMAS
//***********************
// _id property is always assumed
PersonSchema = new Schema({
  name: String,
  age: Number,
  dog: { type: Schema.Types.ObjectId, ref: "Dog" }, // use the model name
})

DogSchema = new Schema({
  name: String,
  breed: String,
  age: Number,
  person: { type: Schema.Types.ObjectId, ref: "Person" }, // use the model name
})

//***********************
// CREATE THE MODELS
//***********************

const Person = model("Person", PersonSchema)
const Dog = model("Dog", DogSchema)
```

Then when querying these models we can "Populate" these records like so.

```js
const dog = Dog.findById(1).populate("person") //using the property name
const person = Person.findById(1).populate("dog") //using the property name
```

##### One to Many Relationship

In a one to many relationship...

Example: One Person can have many dogs

- Person would have an array of ids

- Dog would have a single person id property

## Example

```js
const { Schema, model } = require("mongoose")

//***********************
// CREATE THE SCHEMAS
//***********************
// _id property is always assumed
PersonSchema = new Schema({
  name: String,
  age: Number,
  dogs: [{ type: Schema.Types.ObjectId, ref: "Dog" }], // use the model name
})

DogSchema = new Schema({
  name: String,
  breed: String,
  age: Number,
  person: { type: Schema.Types.ObjectId, ref: "Person" }, // use the model name
})

//***********************
// CREATE THE MODELS
//***********************

const Person = model("Person", PersonSchema)
const Dog = model("Dog", DogSchema)
```

Then when querying these models we can "Populate" these records like so.

```js
const dog = Dog.findById(1).populate("person") //using the property name
const person = Person.findById(1).populate("dogs") //using the property name
```

##### Many to Many Relationship

In a one to one relationship both models would have array of ids!

## Example

```js
const { Schema, model } = require("mongoose")

//***********************
// CREATE THE SCHEMAS
//***********************
// _id property is always assumed
PersonSchema = new Schema({
  name: String,
  age: Number,
  dogs: [{ type: Schema.Types.ObjectId, ref: "Dog" }], // use the model name
})

DogSchema = new Schema({
  name: String,
  breed: String,
  age: Number,
  persons: [{ type: Schema.Types.ObjectId, ref: "Person" }], // use the model name
})

//***********************
// CREATE THE MODELS
//***********************

const Person = model("Person", PersonSchema)
const Dog = model("Dog", DogSchema)
```

Then when querying these models we can "Populate" these records like so.

```js
const dog = Dog.findById(1).populate("persons") //using the property name
const person = Person.findById(1).populate("dogs") //using the property name
```