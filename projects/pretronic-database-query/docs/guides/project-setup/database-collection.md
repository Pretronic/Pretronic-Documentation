---
title: Database collection
---

# Database collection

The database collection holds an undefined amount of entries. It is been created with a predefined schema. From the database
object, the database collection can be got. 

## Create a database collection in a database

````java
DatabaseCollection customers = database.createCollection("customers")
                .field("id", DataType.INTEGER, FieldOption.AUTO_INCREMENT, FieldOption.PRIMARY_KEY)
                .field("name", DataType.STRING, FieldOption.NOT_NULL, FieldOption.INDEX)
                .field("firstName", DataType.STRING, FieldOption.NOT_NULL)
                .field("verified", DataType.BOOLEAN)
                .field("phoneNumber", DataType.STRING)
                .create();  
````

## Queries

!!! note
    Below are some very simple example queries, for more information and more advanced queries, show in the
    [queries section]({{site.site_url}}/guides/queries/).

### Insert query

This query inserts a new collection entry with the name `Shephard` and the firstName `Bill`. The database collection
fields `verified` and `phoneNumber` are null. The id will be generated automatically by your database.

````java
int generatedId = customers.insert()
                .set("name", "Shepard")
                .set("firstName", "Bill")
                .executeAndGetGeneratedKeyAsInt("id");
````

### Find query

This query searches for a collection entry, where the value of the field `name` equals `Shepard`. In the next step,
the result size is printed and is being looped and all fields are printed. 

!!! note
    In some databases, like MySQL, the where operator is equals ignore case by default. Equals ignore case should be
    changed on database side.

````java
FindQuery byName = customers.find().where("name", "Shepard");
QueryResult result = byName.execute();
System.out.println(result.size());
result.forEach(entry -> {
    int id = entry.getInt("id");
    String name = entry.getString("name");
    String firstName = entry.getString("firstName");
    boolean verified = entry.getBoolean("verified");
    String phoneNumber = entry.getString("phoneNumber");
});
````

### Update query

This query updates all entries fields `phoneNumber` to `+49 000000` and `verified` to `true`, where the `firstName`
equals `Bill`.

````java
customers.update()
        .set("phoneNumber", "+49 000000")
        .set("verified", true)
        .where("firstName", "Bill").execute();
````

### Delete query

This query deletes all entries, where the field `firstName` equals `Bill`.

````java
collection.delete()
        .where("firstName", "Bill").execute();
````