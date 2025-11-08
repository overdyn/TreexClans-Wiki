# Getting Started

{% tabs %}
{% tab title="Maven" %}
#### <mark style="color:$primary;">Repository</mark> <a href="#repository-1" id="repository-1"></a>

{% code lineNumbers="true" %}
```xml
<repository>
    <id>jetby-repo</id>
    <url>https://maven.jetby.space</url>
</repository>
```
{% endcode %}

#### &#x20;<mark style="color:$primary;">Dependency</mark>

{% code lineNumbers="true" %}
```xml
<dependency>
    <groupId>space.jetby.TreexClans</groupId>
    <artifactId>api</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```
{% endcode %}
{% endtab %}

{% tab title="Gradle" %}
#### <mark style="color:$primary;">Repository</mark> <a href="#repository-1" id="repository-1"></a>

{% code lineNumbers="true" %}
```xquery
repositories {
    maven { url "https://maven.jetby.space" }
}
```
{% endcode %}

#### &#x20;<mark style="color:$primary;">Dependency</mark>

{% code lineNumbers="true" %}
```gradle
dependencies {
    compileOnly("space.jetby.TreexClans:api:1.0.0")
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

\
