---
title: Driver setup
---

# Introduction

The driver is the base of the database connection. From it, you can get databases. It is created with minimum of a
driver config and a name.

# Create a driver

````java
DatabaseDriver driver = DatabaseDriverFactory.create("MyDriver", driverConfig, logger);
````