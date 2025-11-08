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

| Event Name      |                                                                                                                                                                               | ⚙️ Triggered When                                                 | 🚫 Cancellable |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | -------------- |
| ClanCreateEvent | <p>Fired when a new clan is being created through the TreexClans system.</p><p>Addons can validate, modify, or cancel the creation process before the clan is registered.</p> | When a player or script attempts to create a new clan.            | ✅ Yes          |
| ClanDeleteEvent | <p>Fired when a clan is about to be deleted or disbanded.</p><p>Addons can perform cleanup tasks, prevent deletion, or restore a previously cancelled deletion.</p>           | When a clan is scheduled for removal (manually or automatically). | ✅ Yes          |

<figure><img src="../../../.gitbook/assets/AddonListener.java---Bukkit-Listening.png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

