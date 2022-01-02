---
title: Find Query
---

# Find Query

The find query is used to get entries from the database. For more information about filtering,
see on the [search query page]().

## Getting entries

!!! note
    If you don't specify, which collection fields should be got, all collection fields will be returned

!!! note
    Every time, where a collection is a parameter, you could choose between the database collection object or just 
    the name as a string
### Simple getting

To simple get fields, just write all fields in the get method as strings.

````java
query.get("field1", "field2", "field3")
````

### Getting fields from specific database collection

This is used, if you join in multiple database collections, and one collection field is multiple times represented.

````java
query.get(collection, "id")
````

### Getting with an alias

This is used, if you want to have another name of the field in your result. It is needed, if you want to get two or
more fields, which are multiple represented in the result, for example because of a join.

````java
query.get("field1", "someOtherName")
````

This is also available with a database collection.

````java
query.get(collection, "field1", "someOtherName")
````

### Getting with an aggregation

This is used, if you would like to handle your result with an aggregation, like summing all numbers of a field.

````java
query.get(Aggregation.SUM, "money")
````

### Getting with a function

query.getFunction(yourFunction, "returnName")

These functions are available

#### RowNumberQueryFunction

QueryFunction.rowNumberFunction(orderField, order)