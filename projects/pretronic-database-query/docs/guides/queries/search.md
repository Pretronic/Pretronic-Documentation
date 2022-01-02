---
title: Search Query
---

# Search Query

The search query is the base query of all queries, which can filter. These are the delete, find, update and replace query.
It is used to filter the result on database side.

## Query operations

### Simple selecting

The simplest query is to only filter with one collection field.

````java
QueryResult result = collection.find().where("name", "Shepard").execute();
````

### Negation

To negate a part of a query, you can use the `not` method in the query. Then you would write in the query consumer all
the query part on the given position, which should be negated. For some operations, there are default negation method
implementation, so you have a shorter query.

````java
query.not(query -> query.where("name", "Thomas"))
````

For the `where` operator and other operators are, as it is explained above shorter ways to build the query. For more
short query parts, see the [javadocs](https://javadocs.pretronic.net/pretronic-databasequery/1.1.0.24/net/pretronic/databasequery/api/query/type/SearchQuery.html).

### And/Or queries

`And` and `or` operations are used to specify multiple conditions for the query. All query parts in these queries are
connected with the keyword.

````java
query.and(query -> query.where("name", "Thomas").where("gender", "MALE"))

query.or(query -> query.where("name", "Thomas").where("name", "Peter"))
````

### Limit the result

For limiting the result size, there are several options to use. It is recommended to limit your result size to prevent
an out of memory exception on your client. 

!!! warning
    You can only use limit one time in the query

````java
query.limit(1000)
````

To get all results in pagination, there are some useful query tools to make it easier.

````java
query.page(page, entriesPerPage)
````

You can also get entries with a range of indices.

````java
query.index(startIndex, endIndex)
````

### Order the result

There are many use cases to order a result. You can order your result ascending or descending. 

!!! info
    You can use order by multiple times in the query

````java
query.orderBy(fieldToOrder, SearchOrder.ASC/DESC)
````

Also, you can order with an aggregation.

## Handling the query result

A query results holds multiple result entries. One query has one result with multiple result entries, where one
result entry belongs to one single result (In sql typically one row).

### Checking size

Before you should work with the result entries, you should check if the result has entries.

!!! note
    In this example, only one result entry is got. To get all entries, you should loop through the result

````java
if(!result.isEmpty()) {
    //Do some stuff
    QueryResultEntry resultEntry = result.first();
}
````

### Getting objects from result entry

Every result entry is sorted and one can get values with their index or key.

````java
String name = resultEntry.getString("name");
````