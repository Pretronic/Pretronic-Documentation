---
title: Data Types
---
 
# Data Types

Data Type are the specific data type for a database collection field. While reading or inserting, there can be converted
with DataType Adapters (Show below).

## List of data types

| DataType | Description |
| -------| ----------------------------------------------------------------------|
| `DOUBLE` | Represent decimal numbers |
| `DECIMAL` | Represent decimal numbers |
| `FLOAT` | Represent decimal numbers |
| `INTEGER` | Represent numbers |
| `LONG` | Represent long numbers |
| `CHAR` | Represent short amount of characters |
| `STRING` | Represent a set of characters |
| `LONG_TEXT` | Represent a very long text, in most sql databases, the max size of the column would be multiple gb |
| `DATE` | Represent the java date |
| `DATETIME` | Represent the datetime |
| `TIMESTAMP` | Represent the sql timestamp, it can be got from timestamp long |
| `BINARY` | Represent all binary data |
| `UUID` | Represent uuid class in java, by default the uuid will be converted to binary |
| `BOOLEAN` | Represent boolean |

## DataType Adapter

A data type adapter convert a specific java class to another at inserting and converts it back by reading from the result.

### Create an own adapter

In this example, the preregistered uuid type adapter is used. View the [UUIDTypeAdapter](https://github.com/Pretronic/PretronicDatabaseQuery/blob/master/pretronicdatabasequery-api/src/main/java/net/pretronic/databasequery/api/datatype/adapter/defaults/UUIDDataTypeAdapter.java) example at github.

#### Write operation

The write method will be called by inserting, finding, deleting and updating a value.

````java
@Override
public Object write(UUID value) {
    byte[] uuidBytes = new byte[16];
    ByteBuffer.wrap(uuidBytes)
            .order(ByteOrder.BIG_ENDIAN)
            .putLong(value.getMostSignificantBits())
            .putLong(value.getLeastSignificantBits());
    return uuidBytes;
}
````

#### Read operation

The read operation will be called by using the getObject(key/index, javaClass) method in QueryResultEntry. If there is
no adapter registered for the class, an exception will be throwed.

````java
@Override
public UUID read(Object value) {
    return Convert.toUUID(value);
}
````

### Default data type adapters

By default, there are several data type adapters registered. On your choice, you can register and unregister all adapters
at runtime.

Default adapters:
- UUID
- InetSocketAddress
- InetAddress