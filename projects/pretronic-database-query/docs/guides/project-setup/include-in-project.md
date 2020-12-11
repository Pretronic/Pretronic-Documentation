---
title: Include in your project
---

# Include in your project

There are several options to include pretronic database query into your project. In this example below, we show it with
maven and gradle.

!!! note
    You have to include your jdbc drivers, for example mysql or h2 portable.

## Repository

=== "Maven"

    ``` xml
    <repository>
        <id>pretronic</id>
        <url>https://repository.pretronic.net/repository/pretronic/</url>
    </repository>
    ```

=== "Gradle"

    ```
    repositories {
        maven {
            url "https://repository.pretronic.net/repository/pretronic/"
        }
    }
    ```

## Dependencies

!!! note
    Replace ``VERSION`` with your desired version

### Only api

=== "Maven"

    ``` xml
    <dependency>
        <groupId>net.pretronic.databasequery</groupId>
        <artifactId>pretronicdatabasequery-api</artifactId>
        <version>VERSION</version>
        <scope>compile</scope>
    </dependency>
    ```

=== "Gradle"

    ```
    dependencies {
        compile 'net.pretronic.databasequery:pretronicdatabasequery-api:VERSION'
    }
    ```


### For sql

=== "Maven"

    ``` xml
    <dependency>
        <groupId>net.pretronic.databasequery</groupId>
        <artifactId>pretronicdatabasequery-sql</artifactId>
        <version>VERSION</version>
        <scope>compile</scope>
    </dependency>
    ```

=== "Gradle"

    ```
    dependencies {
        compile 'net.pretronic.databasequery:pretronicdatabasequery-sql:VERSION'
    }
    ```
