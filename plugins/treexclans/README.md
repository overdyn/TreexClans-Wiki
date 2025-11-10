---
icon: '2'
---

# TreexClans



<details>

<summary>Placeholder</summary>

{% hint style="success" %}
**Clan Leaderboard Placeholders**
{% endhint %}

<table><thead><tr><th width="399">Placeholder</th><th>Description</th></tr></thead><tbody><tr><td><code>%clan_top_kills_&#x3C;position>_&#x3C;name/progress></code></td><td>Top by <strong>kills</strong></td></tr><tr><td><code>%clan_top_deaths_&#x3C;position>_&#x3C;name/progress></code></td><td>Top by <strong>deaths</strong></td></tr><tr><td><code>%clan_top_kd_&#x3C;position>_&#x3C;name/progress></code></td><td>Top by <strong>K/D ratio</strong></td></tr><tr><td><code>%clan_top_balance_&#x3C;position>_&#x3C;name/progress></code></td><td>Top by <strong>balance</strong></td></tr><tr><td><code>%clan_top_level_&#x3C;position>_&#x3C;name/progress></code></td><td>Top by <strong>level</strong></td></tr><tr><td><code>%clan_top_members_&#x3C;position>_&#x3C;name/progress></code></td><td>Top by <strong>member count</strong></td></tr></tbody></table>

{% code title="DecentHolograms/holograms/jetbyClanTop.yml" %}
```yaml
location: world:0.500:100.0:0.500
enabled: true
display-range: 64
update-range: 64
update-interval: 20
facing: 0.0
down-origin: false
pages:
- lines:
  - content: "&6Top Clans by Kills:"
    height: 0.3
  - content: "&e#1 &f%clan_top_kills_1_name% &7- &c%clan_top_kills_1_progress% kills"
    height: 0.3
  - content: "&e#2 &f%clan_top_kills_2_name% &7- &c%clan_top_kills_2_progress% kills"
    height: 0.3
  - content: "&e#3 &f%clan_top_kills_3_name% &7- &c%clan_top_kills_3_progress% kills"
    height: 0.3
```
{% endcode %}

</details>

