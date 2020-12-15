---
title: Delete Query
---

# Delete Query

The delete query is used to delete one or many entries in a database collection. For more information about filtering, 
see on the [search query page]().

````java
collection.delete().where("name", "Shepard").execute();
````