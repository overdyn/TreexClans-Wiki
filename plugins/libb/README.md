---
icon: book
---

# Libb

#### Source code: [https://github.com/MrJetby/Libb](https://github.com/MrJetby/Libb)

#### Requirements:

* Java: 17 and higher
* Minecraft version: 1.20 and higher

{% tabs %}
{% tab title="Gradle" %}
{% hint style="danger" %}
The plugin supports addons compiled with **`Java 17`** or higher, provided that the server is running on a Java version not lower than the one used to compile the addon.
{% endhint %}

```css
repositories {
    maven {
        url "http://api.jetby.space/"
        name "jetby-repo"
    }
}

dependencies {
    compileOnly "me.jetby:Libb:1.0"
}
```
{% endtab %}

{% tab title="Maven" %}
{% hint style="danger" %}
The plugin supports addons compiled with <mark style="background-color:red;">**`Java 17`**</mark> or higher, provided that the server is running on a Java version not lower than the one used to compile the addon.
{% endhint %}

```xml
<repository>
  <id>jetby-repo</id>
  <url>http://api.jetby.space/</url>
</repository>

<dependency>
  <groupId>me.jetby</groupId>
  <artifactId>Libb</artifactId>
  <version>VERSION</version>
  <scope>provided</scope>
</dependency>
```
{% endtab %}
{% endtabs %}

