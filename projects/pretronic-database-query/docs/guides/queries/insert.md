---
title: Insert Query
---

The insert query is used to add new rows into your database, there are different possibilities to that.



## Insert a single value

```java

employees.insert()
        .set("Name", "McCain")
        .set("FirstName", "Jack")
        .set("ManagerId", 34)
        .set("Active", true)
        .execute("Id");

```

```java

int id = employees.insert()
        .set("Name", "McCain")
        .set("FirstName", "Jack")
        .set("ManagerId", 34)
        .set("Active", true)
        .executeAndGetGeneratedKeyAsInt("Id");

```

## Insert multiple values

```java

employees.insert()
        .set("Name", "McCain", "Bill")
        .set("FirstName", "Jack", "Shepard")
        .set("ManagerId", 34, 48)
        .set("Active", true, true)
        .execute();
```
