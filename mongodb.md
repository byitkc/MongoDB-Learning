# MongoDB Commands

## Show Databases

`show dbs`

Returns a full list of databases on the Mongo server

## Select Database to Use

`use <dbname>`

Selects the database to be used. Database doesn't have to exist, if the database doesn't exist, it will only be created after making a collection.

## Making a collection

`db.createCollection("<collname>")`

Creates a collection in the current database that is selected / in use.

## Insert Data into Collection

`db.<collname>.insertOne({"name": "example"})`

Inserting one itesm

`db.<collname>.insertMany([{"name": "example1"},{"name": "example2"}])`

Inserting many documents. You can also use multiple lines in the Mongo Shell

``` javascript
db.<collname>.insertMany([
    {"name": "example1"},
    {"name": "example2"}
])
```

You can also use a different syntax for this like the following. It works with other methods as well!

`db.getCollection('<collname>').insertOne({"name": "example3"})`

## Query for Data

### Basic Query

To find one (only returns the first matching result)

`db.<collname>.find({"name": "example1"})`

To find many (returns all matching results)
`db.<collname>.findMany({"name": "example1"})`

### Query Operators

There are available Query operators:

- `$or`
- `$and`
- `$in` - check to see if a value matches a value _in_ an array
- `$eq`
- `$ne`
- `$nin`
- `$lt`
- `$le`
- `$gt`
- `$ge`
- `$regex`

When using a query parameter you should pass it as an object with the operator as the key and the query as the value.

`db.<collname>.find({comments: {$lt: 5}})`

#### Using `$and`/`$or`

``` javascript
db.<collname>.find({
    $and: [
        {comments: {$lt: 5}},
        {comments: {$gt: 0}}
    ]
})
```

#### Using `$in`

``` javascript
db.<collname>.find({
    tags: {
        $in: [
            "programming",
            "coding"
        ]
    }
})
```

## `sort()`, `limit()`, and `skip()` Methods

Keep in mind, that sort, limit, and skip can be chained together like:

`db.<collname>.find({}).skip(2).sort({commants: 1})`

Skips the first two returned documents and sorts ascending.

You can also psplit across several lines to make it more readable

``` javascript
db.<collname>
    .find({})
    .skip(2)
    .sort({shared: 1})
```

### Sort

Will sort resulting documents

`db.<collname>.find({}).sort({commants: 1})`

`1` = Ascending
`-1` = Descending

### Limit

Will limit how many documents are return

`db.<collname>.find({}).limit(2)`

Returns only the first two documents that match the query

### Skip

Will skip the first x documents that are returned

`db.<collname>.find({}).skip(2)`

Skips the first two documents that are returned

## Update Operations

There are two methods:

- `updateOne()`
- `updateMany()`

The you provide the `(<query>, <update>, <options>)`. Each of those is an object

