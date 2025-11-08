# Main config

<pre class="language-yaml"><code class="lang-yaml">storage:
  # YAML, MYSQL, SQLITE, JSON
  type: "YAML"
  #
  # If type is set to YAML or JSON
  #
<strong>  # If you have a large online, it is recommended to enable this option to avoid loading the server when working with YAML/JSON
</strong>  # true - Will instantly save data to a file when changing
  # false - Will save data to a file only when the server is rebooted
<strong>  # If you have a small online, you can leave false
</strong>  yaml-or-json-force-save: false
  # The data below is used for MYSQL only.
  host: "localhost"
  port: 3306
  database: "treexbuyer"
  username: "root"
  password: ""

debug: false

autobuy:
  delay: 60  # In ticks. How often AutoBuy will be triggered. Default is 60 - 3 seconds
  actions:
    - '[MESSAGE] &#x26;8&#x26;l> &#x26;fn Automatically sold items worth &#x26;a&#x26;l%sell_pay%&#x26;f, and &#x26;c&#x26;l%sell_score% &#x26;fpoints.'
  disabled-worlds:
    - duel-1
    - duel-2
  status:
    enable: "&#x26;aEnabled"
    disable: "&#x26;cDisabled"


score-system:
  # How will the Coefficient grow
  # GLOBAL - For all subjects at once
  # ITEM - For each subject its own
  # CATEGORY - For each category its own
  type: GLOBAL
  multiplier-ratio:
    scores: 100
    coefficient: 0.01

  # maximum coefficient (excluding donation boosts)
  default-coefficient: 1
  max-legal-coefficient: 3

  # if true, donation boosts will bypass the value in max-legal-coefficient
  boosters_except_legal_coefficient: true

  booster:
    donat-1: # name (can be any)
      permission: 'buyer.boost.donat1' # (permission by which the presence of a boost will be determined)
      external-coefficient: 0.5


</code></pre>
