# AdvancedCommand

Extend the class:

```java
public class TestCommand extends AdvancedCommand {

    public TestCommand(JavaPlugin plugin) {
        super("test_command", plugin);
    }
}
```

`"test_command"` is the name of the command on the server.

If you need to handle this command, use **`onExecute`**. Importantly, do **not** use `onCommand`, as it is an integral part of the utility's core logic. Modify this **only** if you know exactly what you are doing. The same applies to `onTabComplete`; **instead**, use `onTab`.



onExecute usage:

```java
public class TestCommand extends AdvancedCommand {

    public TestCommand(JavaPlugin plugin) {
        super("test_command", plugin);
    }
    @Override
    public boolean onExecute(CommandSender sender, Command command, String label, String[] args) {
        sender.sendMessage("Success");
        return true;
    }
}
```

onTab usage

```java
public class TestCommand extends AdvancedCommand {

    public TestCommand(JavaPlugin plugin) {
        super("test_command", plugin);
    }
    @Override
    public List<String> onTab(CommandSender sender, Command command, String label, String[] args) {
        return List.of("help");
    }
}
```

Or you can use both:

```java
public class TestCommand extends AdvancedCommand {

    public TestCommand(JavaPlugin plugin) {
        super("test_command", plugin);
    }
    @Override
    public boolean onExecute(CommandSender sender, Command command, String label, String[] args) {
        sender.sendMessage("Success");
        return true;
    }
    @Override
    public List<String> onTab(CommandSender sender, Command command, String label, String[] args) {
        return List.of("help");
    }
}
```
