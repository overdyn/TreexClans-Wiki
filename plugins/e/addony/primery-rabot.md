# Примеры работ

## 🧩 Разработка аддонов для TreexClans

{% stepper %}
{% step %}
### Как выключить плагин

> Используя метод <mark style="color:$warning;">this.getServiceManager().getAddonManager().disable(this);</mark>, вы можете отключить как собственный аддон, так и любой другой, переданный в параметре. Класс при этом обязательно должен наследоваться от `JavaAddon`.

<figure><img src="../../../.gitbook/assets/AddonManager.class(1) (2).png" alt="" width="188"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
###


{% endstep %}
{% endstepper %}

Добро пожаловать в **Addon Development Guide** — официальное руководство по созданию аддонов (модулей) для системы **TreexClans**.

Аддоны позволяют расширять функционал кланов без изменения основного плагина:

* новые команды и подкоманды;
* собственные GUI и меню;
* интеграции с другими плагинами;
* квесты, рейтинги, экономика, визуал;
* любые свои игровые механики поверх клан-системы.

***

## 📦 Где хранятся аддоны

Все аддоны TreexClans — это отдельные `.jar`-файлы, которые загружаются из директории:

```
/plugins/TreexClans/addons/
```

Пример структуры сервера:

```
plugins/
 └── TreexClans/
      └── addons/
           ├── ExampleAddon.jar
           ├── ClanShopAddon.jar
           └── ClanEventsAddon.jar
```

Правила:

* один `.jar` = один аддон;
* для обновления аддона замените `.jar` и перезапустите сервер;
* TreexClans автоматически сканирует папку `addons` и инициализирует найденные аддоны.

***

## ⚙️ Что такое аддон TreexClans

**Аддон TreexClans** — это мини-плагин, который:

* подключается к ядру TreexClans;
* использует предоставленный **API**;
* живёт в своём `.jar` и не ломает основной плагин.

Что можно сделать аддоном:

* добавить клановый магазин;
* ввести прокачку перков клана;
* сделать свои GUI для управления кланом;
* связать кланы с другими системами (донат, статистика, ивенты);
* расширить события, логирование и обработку действий игроков.

***

## 🧱 Базовая структура аддона

Минимально аддон должен иметь:

* главный класс, наследующийся от `JavaAddon`;
* аннотацию `@ClanAddon` на этом классе;
* корректно собранный `.jar` и размещение в `/plugins/TreexClans/addons/`.

Пример минимального аддона:

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

Ключевые моменты:

* `@ClanAddon` — **обязательна**. Без неё аддон не будет обнаружен.
* `id` — уникальный идентификатор аддона.
* Класс должен **extends JavaAddon**.
* `onEnable()` / `onDisable()` — точки входа жизненного цикла аддона.

***

## 🔗 Подключение TreexClans API

Чтобы использовать API TreexClans в своём проекте, нужно добавить зависимость.

{% tabs %}
{% tab title="Maven" %}
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

{% tab title="Gradle" %}
```groovy
repositories {
    maven { url "https://maven.jetby.space" }
}

dependencies {
    compileOnly("space.jetby.TreexClans:api:1.0.0")
}
```
{% endtab %}
{% endtabs %}

Рекомендации:

* используйте `provided` / `compileOnly`, чтобы API не встраивался в `.jar` аддона;
* на сервере API уже доступен внутри основного TreexClans.

***

## 🧭 Доступ к сервисам TreexClans

Через `JavaAddon` вы получаете доступ к контексту и сервисам.

Получение `ServiceManager`:

```java
var service = getContext().getServiceManager();
```

Основные методы `ServiceManager`:

```java
var plugin        = service.getPlugin();
var dataFolder    = service.getDataFolder();
var clanManager   = service.getClanManager();
var leaderboard   = service.getLeaderboardService();
var commandSvc    = service.getCommandService();
var guiFactory    = service.getGuiFactory();
var configService = service.getServiceConfiguration();
var addonManager  = service.getAddonManager();
```

Пример: получить клан игрока и отправить ему сообщение:

```java
var clan = clanManager.getClanByMember(player.getUniqueId());
if (clan != null) {
    player.sendMessage("Вы состоите в клане: " + clan.getId());
} else {
    player.sendMessage("Вы не состоите в клане.");
}
```

***

## 🎨 GUI и меню

TreexClans API предоставляет инструменты для создания собственных GUI, основанных на его системе меню.

Пример регистрации GUI-типа:

```java
var guiService = service.getGuiFactory().getGuiService();

guiService.registerGui("EXAMPLE_MENU", (plugin, menu, player, clan, args) ->
        new ExampleGui(plugin, menu, player, clan)
);
```

Пример GUI:

```java
import me.jetby.treexclans.api.gui.Gui;
import me.jetby.treexclans.api.gui.Menu;
import me.jetby.treexclans.api.service.clan.Clan;
import org.bukkit.entity.Player;
import org.bukkit.plugin.java.JavaPlugin;

public class ExampleGui extends Gui {

    public ExampleGui(JavaPlugin plugin, Menu menu, Player player, Clan clan) {
        super(plugin, menu, player, clan);
        registerButtons();
    }
}
```

***

## ⚙️ Конфигурация аддона

Файлы аддона хранятся в `/plugins/TreexClans/addons/<id_аддона>/`.

Получить основной конфиг:

```java
var cfg = service.getServiceConfiguration().getConfig();
String value = cfg.getString("settings.example");
```

Получить отдельный файл:

```java
var fileCfg = service.getServiceConfiguration().getFileConfiguration("custom.yml");
```

***

## 💻 Команды

Регистрируем подкоманду:

```java
commandService.registerCommand("example", new ExampleSubcommand());
```

```java
public class ExampleSubcommand implements Subcommand {
    @Override
    public boolean onCommand(@NotNull CommandSender sender, @NotNull String[] args) {
        if (sender instanceof Player player) {
            player.sendMessage("Пример подкоманды аддона.");
        }
        return true;
    }
}
```

***

## 🧰 Сборка и загрузка

{% stepper %}
{% step %}
### Подготовка проекта

Настройте проект и зависимости.
{% endstep %}

{% step %}
### Реализация аддона

Реализуйте аддон (`extends JavaAddon`, `@ClanAddon`).
{% endstep %}

{% step %}
### Сборка

Соберите `.jar`.
{% endstep %}

{% step %}
### Копирование на сервер

Поместите его в `plugins/TreexClans/addons/`.
{% endstep %}

{% step %}
### Перезапуск сервера

Перезапустите сервер.
{% endstep %}
{% endstepper %}

Вывод в консоли:

```
[TreexClans] Found addon: example-addon v1.0.0
[TreexClans] Addon example-addon enabled.
```

***

## 💡 Рекомендации

* Проверяйте наличие аннотации `@ClanAddon` и наследование от `JavaAddon`.
* Логируйте через `getLogger()`.
* Не вшивайте API в `.jar`.
* Держите `id` аддона уникальным.

***

## 🚀 Идеи аддонов

| Название       | Описание                         |
| -------------- | -------------------------------- |
| **ClanBank**   | Клановый банк, переводы и лимиты |
| **ClanShop**   | Клановый магазин предметов       |
| **ClanEvents** | Войны и ивенты между кланами     |
| **ClanTop**    | Альтернативная система рейтинга  |
| **ClanQuests** | Клановые задания и награды       |

***

## 📌 Итог

Теперь вы знаете, как:

* подключить TreexClans API;
* создать собственный аддон;
* работать с GUI, командами и сервисами;
* собрать и запустить модуль.

Используйте API TreexClans для создания уникальных механик и расширения игрового процесса!
