# Addons

### 🧩 TreexClans Addons

Welcome to the **Addons** section — this page introduces the modular system of TreexClans.\
Here you’ll learn what addons are, where they’re located, how they work, and what types of addons exist.

The goal of this section is to give you a clear understanding of how TreexClans addons integrate with the core plugin, how they extend functionality, and how you can create your own.

> 📘 A detailed guide on how to create and integrate addons can be found on a separate page — **Addon Development**.

***

### 📖 What Is an Addon

A **TreexClans Addon** is an additional module that extends the functionality of the clan system without modifying the plugin’s core.\
Each addon is a standalone `.jar` file that can be easily installed, removed, or updated at any time.

With addons, you can:

* introduce new features and mechanics for clans;
* add visual or economy-based systems;
* integrate clans with other server plugins or APIs;
* create custom quests, leaderboards, events, and GUI interfaces.

***

#### 📦 Addon Location

All addons are located in the following folder:

```
/plugins/TreexClans/addons/
```

Example structure:

```
plugins/
 └── TreexClans/
      └── addons/
           ├── ClanShop.jar
           ├── ClanTop.jar
           └── ExampleAddon.jar
```

#### 🔧 Basic Rules

* **1 `.jar` file = 1 addon**\
  Each addon is a standalone module packed into a single `.jar` file.
* **Updating an addon**\
  To update an addon, simply replace the old `.jar` file with the new one in the addons folder.
* **Automatic loading**\
  When TreexClans starts, it automatically detects and enables all addons found in the folder.

***

### ⚙️ How the Addon System Works

When TreexClans starts up, it:

1. Scans the `addons/` folder;
2. Checks each file for compatibility;
3. Loads addons in the proper initialization order;
4. Activates them, integrating with the core system.

This way, all modules operate independently while still communicating with TreexClans through a unified API.

***

### 🪶 Advantages of the System

* **Modularity** — each feature is packaged as a separate addon.
* **Flexibility** — you can enable or disable any module at any time.
* **Security** — the plugin’s core remains untouched and protected.
* **Compatibility** — addons operate independently and don’t interfere with one another.
* **Scalability** — the system is easily extendable and built to grow.

***

### 💾 Files and Configuration

Each addon has its own dedicated directory for storing files and configuration data:

***

```
/plugins/TreexClans/addons/<id_аддона>/
```

It may contain:

* **config.yml** — the main configuration file;
* additional **.yml** files (for example: settings, data, or quests);
* cache, temporary, and auxiliary files.

This structure is created automatically when the addon is launched for the first time.

***

### ⚖️ Compatibility and Dependencies

Some addons may depend on others.\
If a required module is missing or incompatible, TreexClans will notify you in the console and skip loading any addons that depend on it.

> 🔍 The system manages the loading order to ensure that all modules start correctly and without conflicts.

***

### 💡 Примеры встроенных и популярных аддонов

| 🔧 Addon Name  | 📝 Addon Description                          |
| -------------- | --------------------------------------------- |
| **ClanShop**   | Клановый магазин предметов, валют и апгрейдов |
| **ClanQuests** | Система заданий и достижений клана            |
| **ClanEvents** | Ивенты, сражения и PvP‑механики               |
| **ClanTop**    | Альтернативные рейтинги и лидерборды          |
| **ClanBank**   | Клановый банк и система переводов             |
| **ClanDecor**  | Настройка внешнего вида и символики клана     |

> 🧩 This list includes only examples — addons can be either built-in or created by third-party developers.

***

### 🚀 Why Addons Matter

Addons make TreexClans a complete ecosystem, where every part of the system can function as a separate module:

* **Administrators** can flexibly manage and customize functionality;
* **Developers** can add their own ideas without modifying the core;
* **Servers** can adapt the system to their unique gameplay style — whether it’s RPG, Grief, SMP, or anything else.

***

### 📌 What’s Next

If you want to learn:

* how to create your own addons;
* how to connect and use the TreexClans API;
* how to integrate services and commands —

then head over to the **Addon Development** page.

***

© TreexClans API — a powerful and flexible extension system for Minecraft servers.
