---
title: Include in your project
---

# Include in your project

There are several options to include pretronic database query into your project. In this example below, we show it with
maven and gradle.

Important:
You have to include your jdbc drivers, for example mysql or h2 portable.

## Maven
```xml
<repository>
    <id>pretronic</id>
    <url>https://repository.pretronic.net/repository/pretronic/</url>
</repository>
```

Only for api:
```xml
<dependency>
    <groupId>net.pretronic.databasequery</groupId>
    <artifactId>pretronicdatabasequery-api</artifactId>
    <version>VERSION</version>
    <scope>compile</scope>
</dependency>
```

For sql:
```xml
<dependency>
    <groupId>net.pretronic.databasequery</groupId>
    <artifactId>pretronicdatabasequery-api</artifactId>
    <version>VERSION</version>
    <scope>compile</scope>
</dependency>
```

## Gradle
```xml
repositories {
    maven {
        url "https://repository.pretronic.net/repository/pretronic/"
    }
}
```

Only for api:
```xml
dependencies {
    compile 'net.pretronic.databasequery:pretronicdatabasequery-api:VERSION'
}
```

For sql:
```xml
dependencies {
    compile 'net.pretronic.databasequery:pretronicdatabasequery-sql:VERSION'
}
```