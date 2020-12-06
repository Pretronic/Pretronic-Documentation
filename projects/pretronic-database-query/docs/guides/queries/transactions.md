---
title: Transactions
---

A transaction is a series of different queries that are related to each other and are executed in different steps of 
the application logic. Transaction gives you the possibilities to rollback your database actions if your code fails, or 
you want user give an option to cancel an ongoing process.

## Use case

Transactions are normally used when multiple queries need to be executed without any errors.
A simple example is moving an amount form one bank account to another. 
Both queries must be completed successfully in order not to lose money or generate duplicate amounts.

# Open a new transaction

A new transaction is opened with `.transact()` on a database or collection object. 
A transaction is alive until it is committed or rollbacked, after that you have to open a new transaction.

Unlike using `.execute()` on the query itself, you pass your query to the transaction object.
The transaction will then execute the query in an isolated thread on the database.

Note: For each transaction a new reserved connection to the database is opened.

```java

QueryTransaction transaction = database.transact()

transaction.execute(balances.update().add("Id",9.99).where("Id",6562));

```

# Commit a transaction

When your process is completed and all queries have been executed, close the transaction with `.commit()`
to tell the database that everything worked. 

```java
transaction.commit();
```

# Rollback a transaction

Should your code fail or a user aborts the process, use `.rollback()` to tell the database to cancel 
everything, changes will than no longer apply. This part is usually placed in a catch statement.

```java
transaction.rollback();
```


# Sample implementation

This code below shows a small example of how to use a transaction.

```java

Database database = driver.getDatabase("Bank");
DatabaseCollection balances = database.getCollection("balances");

QueryTransaction transaction = database.transact();

try{
    //Perform your queries
    transaction.execute(balances.update().add("Id",9.99).where("Id",6562));
    transaction.execute(balances.update().subtract("Id",9.99).where("Id",7830));

    //Cou can also include normal java code


    transaction.commit();//The code succeeded
}catch (Exception exception){
    transaction.rollback();//Something failed, rollback the transaction (Changes will not apply in the database)
    throw exception;
}

```
