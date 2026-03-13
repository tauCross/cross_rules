# cross_rules

* mihomo
    ```
    rule-providers:
      cross_block:
        type: http
        behavior: classical
        format: text
        path: ./ruleset/cross_block.list
        url: "https://raw.githubusercontent.com/tauCross/cross_rules/refs/heads/main/block.list"
        interval: 3600

      cross_proxy:
        type: http
        behavior: classical
        format: text
        path: ./ruleset/cross_proxy.list
        url: "https://raw.githubusercontent.com/tauCross/cross_rules/refs/heads/main/proxy.list"
        interval: 3600

    rules:
      - DOMAIN-SUFFIX,githubusercontent.com,Proxy

      - RULE-SET,cross_block,REJECT
      - RULE-SET,cross_proxy,Proxy
      - MATCH,DIRECT
    ```