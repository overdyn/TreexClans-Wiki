# Addon Development

### ⚙️ TreexClans Addon Development

Welcome to the **TreexClans Addon Development Guide**.\
Here you’ll learn how to create your own addon, connect it to the API, set up dependencies, and correctly build your `.jar` file.

> 🧠 This page is intended for developers.\
> If you just want to learn what addons are, see the **Addons Overview** page.

***

### 📦 Connecting the TreexClans API

To use the TreexClans API in your project, add the repository and dependency to your build system.



{% tabs %}
{% tab title="Gradle" %}
{% hint style="danger" %}
The plugin supports addons compiled with **`Java 17`** or higher, provided that the server is running on a Java version not lower than the one used to compile the addon.
{% endhint %}

{% hint style="warning" %}
Use `compileOnly` so that the API is not included inside your `.jar` file.
{% endhint %}

```css
repositories {
    maven {
        name = "jetby-repo"
        url = "https://maven.jetby.space"
    }
    maven {
        name = "jitpack.io"
        url = "https://jitpack.io"
    }
    maven {
        name = "Jodexindustries-releases"
        url = "https://repo.jodex.xyz/releases"
    }
}

dependencies {
    compileOnly("space.jetby.TreexClans:api:2.1")
}
```
{% endtab %}

{% tab title="Maven" %}
{% hint style="danger" %}
The plugin supports addons compiled with <mark style="background-color:red;">**`Java 17`**</mark> or higher, provided that the server is running on a Java version not lower than the one used to compile the addon.
{% endhint %}

{% hint style="warning" %}
Use `provided` so that the API is not included inside your `.jar` file.
{% endhint %}

```xml
<repositories>
    <repository>
        <id>jetby-repo</id>
        <url>https://maven.jetby.space/</url>
    </repository>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
    <repository>
        <id>Jodexindustries-releases</id>
        <url>https://repo.jodex.xyz/releases</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>space.jetby.TreexClans</groupId>
        <artifactId>api</artifactId>
        <version>2.1</version>
        <scope>provided</scope>
    </dependency>
<dependencies>
```
{% endtab %}
{% endtabs %}

***

### 🧱 Project Structure

At minimum, an addon must include:

* a **main class** that extends `JavaAddon`;
* a **@ClanAddon** annotation with basic metadata;
* a valid **plugin.yml** (if required);
* any **resources** or configuration files (if needed).

**Example project structure:**

```
src/
 └── main/
      ├── java/
      │    └── me/jetby/clanWar/
      │         └── ClanWarAddon.java
      │
      └── resources/
           └── config/
                └── messages.yml

```

***

#### 🧩 Basic Addon Example

{% code title="ExampleAddon.java" %}
```java
import me.jetby.treexclans.api.addons.JavaAddon;
import me.jetby.treexclans.api.addons.annotations.ClanAddon;

@ClanAddon(
        id = "clanWar",
        version = "1.0.0",
        authors = {"JetBy"},
        description = "Example addon for TreexClans"
)
public class ExampleAddon extends JavaAddon {

    @Override
    public void onEnable() {
        getLogger().info("clanWar enabled!");
    }

    @Override
    public void onDisable() {
        getLogger().info("clanWar disabled!");
    }
}
```
{% endcode %}

#### 🔑 Key Points

* `@ClanAddon` — required for the addon to be recognized and registered.
* id must be unique among all addons.
* extends `JavaAddon` — defines the entry point of your addon.
* `onEnable()` and `onDisable()` — control the addon’s lifecycle.

***

***

### 🧭 Working with the API and Services

TreexClans provides a **Service Manager**, which can be accessed through the addon’s context:

```java
var service = getContext().getServiceManager();
```

Основные методы:

```java
var clanManager   = service.getClanManager();
var leaderboard   = service.getLeaderboardService();
var commandSvc    = service.getCommandService();
var guiFactory    = service.getGuiFactory();
var addonManager  = service.getAddonManager();
```

Пример — получить клан игрока:

```java
var clan = clanManager.getClanByMember(player.getUniqueId());
if (clan != null) {
    player.sendMessage("You are in a clan: " + clan.getName());
}
```

***

### 🧰 Commands and Interfaces

Adding a subcommand:

```java
commandSvc.registerCommand("example", new ExampleCommand());
```

```java
public class ExampleCommand implements Subcommand {
    @Override
    public boolean onCommand(CommandSender sender, String[] args) {
        if (sender instanceof Player player) {
            player.sendMessage("🧩 Example TreexClans Subcommand");
        }
        return true;
    }
}
```

***

***

#### 🎨 GUI and Menus

The GUI system allows you to create custom menus for player interaction.

Registering a GUI type:

```java
guiService.registerGui("EXAMPLE_MENU", (plugin, menu, player, clan, args) ->
        new ExampleGui(plugin, menu, player, clan)
);
```

Example GUI class:

```java
public class ExampleGui extends Gui {
    public ExampleGui(JavaPlugin plugin, Menu menu, Player player, Clan clan) {
        super(plugin, menu, player, clan);
        registerButtons();
    }
}
```

***

### 🧩 Addon Configuration

TreexClans creates a separate directory for each addon:

```
/plugins/TreexClans/addons/<id_аддона>/
```

Example of getting the configuration:

```java
var cfg = service.getServiceConfiguration().getConfig();
String value = cfg.getString("settings.example");
```

***

### 🏗️ Building and Installation

1. Build your project into a `.jar` file (using **Gradle** or **Maven**).
2. Place the file into `plugins/TreexClans/addons/`.
3. Restart the server or use /xclan reload

The console will display a message:

***

```
[TreexClans] Found addon: example-addon v1.0.0
[TreexClans] Addon example-addon enabled.
```

***

### 💡 Recommendations

* Do **not** embed the TreexClans API inside your `.jar`.
* Always check for the `@ClanAddon` annotation and correct inheritance.
* Use `getLogger()` for logging instead of `System.out`.
* Store configuration and data files inside the addon’s dedicated folder.
* Follow consistent **naming** and **versioning** conventions.

***

### 📘 Summary

Now you know how to:

* connect to the **TreexClans API**;
* create and register your own addon;
* work with **services**, **GUIs**, and **commands**;
* build and install your module on the server.

> 🔗 **Next step** — explore the advanced features of the API: events, dependencies, caching, and database integration.
