---
title: Update Query
---

# Update Query

The update query is used to change some values of entries. For more information about filtering,
see on the [search query page]().

## Replace value

````java
query.update(yourField, yourValue)
````

## Update value

This is used to calculate the value on database side, like adding a number to the value. Only numbers are possible to 
use for number.

````java
query.add(yourField, number)
query.subtract(yourField, number)
query.multiply(yourField, number)
query.divide(yourField, number)
````