# Разработка аддонов

## ⚙️ Разработка аддонов TreexClans

Добро пожаловать в **руководство по разработке аддонов** для TreexClans. Здесь описано, как создать свой аддон, подключить API, настроить зависимости и правильно собрать `.jar`‑файл.

> 🧠 Эта страница предназначена для разработчиков. Если вы просто хотите узнать, что такое аддоны, см. Обзор аддонов.

***

### 📦 Подключение TreexClans API

Чтобы использовать API TreexClans в своём проекте, добавьте репозиторий и зависимость в сборочную систему.



{% tabs %}
{% tab title="Gradle" %}
{% hint style="warning" %}
Используйте `compileOnly`, чтобы API не попадал внутрь вашего `.jar`.
{% endhint %}

```css
repositories {
    maven { url "https://maven.jetby.space" }
}

dependencies {
    compileOnly("space.jetby.TreexClans:api:1.0.0")
}
```
{% endtab %}

{% tab title="Maven" %}
{% hint style="warning" %}
Используйте `provided`, чтобы API не попадал внутрь вашего `.jar`.
{% endhint %}

```xml
<repository>
    <id>jetby-repo</id>
    <url>https://maven.jetby.space</url>
</repository>

<dependency>
    <groupId>space.jetby.TreexClans</groupId>
    <artifactId>api</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```
{% endtab %}
{% endtabs %}

***

### 🧱 Структура проекта

Минимально аддон должен содержать:

* главный класс, наследующийся от `JavaAddon`;
* аннотацию `@ClanAddon` с основными метаданными;
* корректный `plugin.yml` (если требуется);
* ресурсы и конфигурационные файлы (при необходимости).

Пример структуры проекта:

```
src/main/java/
 └── me/yourname/addons/example/
      ├── ExampleAddon.java
      └── config/
          └── messages.yml
```

***

### 🧩 Пример базового аддона

```java
import me.jetby.treexclans.api.addons.JavaAddon;
import me.jetby.treexclans.api.addons.annotations.ClanAddon;

@ClanAddon(
        id = "example-addon",
        version = "1.0.0",
        authors = {"YourName"},
        description = "Пример аддона для TreexClans"
)
public class ExampleAddon extends JavaAddon {

    @Override
    public void onEnable() {
        getLogger().info("ExampleAddon включён!");
    }

    @Override
    public void onDisable() {
        getLogger().info("ExampleAddon выключен!");
    }
}
```

**Ключевые моменты:**

* `@ClanAddon` — обязательна для регистрации аддона.
* `id` должен быть уникальным.
* `extends JavaAddon` — определяет точку входа.
* `onEnable()` и `onDisable()` управляют жизненным циклом.

***

### 🧭 Работа с API и сервисами

TreexClans предоставляет сервис‑менеджер, доступный через контекст аддона:

<img alt="" class="gitbook-drawing">

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
    player.sendMessage("Вы в клане: " + clan.getName());
}
```

***

### 🧰 Команды и интерфейсы

Добавление подкоманды:

```java
commandSvc.registerCommand("example", new ExampleCommand());
```

```java
public class ExampleCommand implements Subcommand {
    @Override
    public boolean onCommand(CommandSender sender, String[] args) {
        if (sender instanceof Player player) {
            player.sendMessage("Пример подкоманды TreexClans!");
        }
        return true;
    }
}
```

***

### 🎨 GUI и меню

Система GUI позволяет создавать собственные меню для взаимодействия с игроками.

Регистрация GUI‑типа:

```java
guiService.registerGui("EXAMPLE_MENU", (plugin, menu, player, clan, args) ->
        new ExampleGui(plugin, menu, player, clan)
);
```

Пример GUI‑класса:

```java
public class ExampleGui extends Gui {
    public ExampleGui(JavaPlugin plugin, Menu menu, Player player, Clan clan) {
        super(plugin, menu, player, clan);
        registerButtons();
    }
}
```

***

### 🧩 Конфигурация аддона

TreexClans создаёт отдельную директорию для каждого аддона:

```
/plugins/TreexClans/addons/<id_аддона>/
```

Пример получения конфига:

```java
var cfg = service.getServiceConfiguration().getConfig();
String value = cfg.getString("settings.example");
```

***

### 🏗️ Сборка и установка

1. Соберите проект в `.jar` (Gradle/Maven).
2. Поместите файл в `plugins/TreexClans/addons/`.
3. Перезапустите сервер.

Консоль выведет сообщение:

```
[TreexClans] Found addon: example-addon v1.0.0
[TreexClans] Addon example-addon enabled.
```

***

### 💡 Рекомендации

* Не вшивайте API TreexClans внутрь `.jar`.
* Проверяйте наличие `@ClanAddon` и корректное наследование.
* Используйте `getLogger()` для логирования.
* Храните конфиги и данные в выделенной папке аддона.
* Придерживайтесь нейминга и версионирования.

***

### 📘 Итог

Теперь вы знаете, как:

* подключить TreexClans API;
* создать и зарегистрировать аддон;
* работать с сервисами, GUI и командами;
* собрать и установить модуль на сервер.

> 🔗 Следующий шаг — изучить продвинутые возможности API: события, зависимости, кэш и работу с базой данных.
