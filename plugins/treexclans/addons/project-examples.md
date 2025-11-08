# Project Examples

## 🧩 Addon Development for TreexClans

{% stepper %}
{% step %}
#### How to Disable a Plugin

{% hint style="success" %}
Using the method <mark style="color:$danger;">**`this.getServiceManager().getAddonManager().disable(this);`**</mark>,\
you can disable either your own addon or any other addon passed as a parameter.\
The class must extend **`JavaAddon`** for this to work.
{% endhint %}

<figure><img src="../../../.gitbook/assets/JebyTestAddon.java(2).png" alt=""><figcaption></figcaption></figure>

\

{% endstep %}

{% step %}
#### 🎯 Listening to TreexClans Events

<table data-view="cards"><thead><tr><th>🧩 Event Name</th><th>📝 Description</th><th>⚙️ Triggered When</th><th>🚫 Cancellable</th></tr></thead><tbody><tr><td><mark style="color:$info;">ClanCreateEvent</mark></td><td><p><mark style="color:$info;">Fired when a new clan is being created through the TreexClans system.</mark></p><p><mark style="color:$info;">Addons can validate, modify, or cancel the creation process before the clan is registered.</mark></p></td><td><mark style="color:$info;">When a player or script attempts to create a new clan.</mark></td><td><mark style="color:$info;">✅ Yes</mark></td></tr><tr><td><sub><mark style="color:$info;">ClanDeleteEvent</mark></sub></td><td><p><mark style="color:$info;">Fired when a clan is about to be deleted or disbanded.</mark></p><p><mark style="color:$info;">Addons can perform cleanup tasks, prevent deletion, or restore a previously cancelled deletion.</mark></p></td><td><mark style="color:$info;">When a clan is scheduled for removal (manually or automatically).</mark></td><td><mark style="color:$info;">✅ Yes</mark></td></tr></tbody></table>

***

<figure><img src="../../../.gitbook/assets/AddonListener.java---Bukkit-Listening.png" alt=""><figcaption></figcaption></figure>


{% endstep %}
{% endstepper %}

