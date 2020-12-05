---
title: Driver config setup
---

# Driver config

The driver config is the base of database driver. It contains the required options to connect the driver to your database.
The driver config is divided into remote database driver config for connecting to remote databases and local database
driver configs for connecting to local databases like file databases. 

## Pre-Requirements

You need a slf4j logger in your runtime. Either you declare a logger on your self, or you can use a PretronicLogger 
and set it as a slf4j logger instance.

Setup a PretronicLogger as slf4j logger instance:
```java
PretronicLogger logger = PretronicLoggerFactory.getLogger();
SLF4JStaticBridge.setLogger(logger);
```

## Create a driver config

There are two options to create a driver config. One option is to load it from a document or from a file and the other 
option is to create a driver config directly from the code. In these examples, we use for the local database config example
h2 portable and for remote MySQL.

### Loading from a document

####Config examples

For a local database:
```yaml
location: 'databases/'
driver: 'net.pretronic.databasequery.sql.driver.SQLDatabaseDriver'
name: 'Default'
dialectName: 'H2Portable'
useSSL: false
```

For a remote database:
```yaml
address: '127.0.0.1'
username: 'root'
password: '******'
driver: 'net.pretronic.databasequery.sql.driver.SQLDatabaseDriver'
name: 'MySQL'
dialectName: 'MySQL'
useSSL: false
```

Load a driver config from a file:
```java
DatabaseDriverConfig<?> config = DatabaseDriverFactory.create(DocumentFileType.YAML.getReader().read(new File("driver-config.yml")));
```

### Create directly from code

Create a h2-portable driver config:
```java
DatabaseDriverConfig<?> config = new SQLDatabaseDriverConfigBuilder()
                .setName("H2-Portable")
                .setLocation(new File("databases/"))
                .setDialect(Dialect.H2_PORTABLE)
                .setUseSSL(false)
                .build();
```

Create a mysql driver config:
````java
DatabaseDriverConfig<?> config = new SQLDatabaseDriverConfigBuilder()
                .setName("MySQL")
                .setAddress(new InetSocketAddress("127.0.0.1", 3306))
                .setDialect(Dialect.MYSQL)
                .setUsername("root")
                .setPassword("'******'")
                .setUseSSL(false)
                .build()
````