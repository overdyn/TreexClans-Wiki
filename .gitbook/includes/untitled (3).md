---
title: Untitled
---

{% tabs %}
{% tab title="Maven" %}
### <mark style="color:$primary;">Repository</mark> <a href="#repository-1" id="repository-1"></a>

```xml
<repository>
    <id>jetby-repo</id>
    <url>https://maven.jetby.space</url>
</repository>
```

### &#x20;<mark style="color:$primary;">Dependency</mark>

```xml
<dependency>
    <groupId>space.jetby.TreexClans</groupId>
    <artifactId>api</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```
{% endtab %}

{% tab title="Gradle" %}
### <mark style="color:$primary;">Repository</mark> <a href="#repository-1" id="repository-1"></a>

```gradle
repositories {
    maven { url "https://maven.jetby.space" }
}
```

### &#x20;<mark style="color:$primary;">Dependency</mark>

```gradle
dependencies {
    compileOnly("space.jetby.TreexClans:api:1.0.0")
}
```
{% endtab %}
{% endtabs %}

*
