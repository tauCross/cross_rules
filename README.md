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

* shadowrocket
  ```
  [General]
  bypass-system = true
  skip-proxy = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, localhost, *.local, captive.apple.com
  tun-excluded-routes = 10.0.0.0/8, 100.64.0.0/10, 127.0.0.0/8, 169.254.0.0/16, 172.16.0.0/12, 192.0.0.0/24, 192.0.2.0/24, 192.88.99.0/24, 192.168.0.0/16, 198.51.100.0/24, 203.0.113.0/24, 224.0.0.0/4, 255.255.255.255/32, 239.255.255.250/32
  dns-server = system
  ipv6 = true
  prefer-ipv6 = false
  dns-fallback-system = false
  dns-direct-system = false
  icmp-auto-reply = true
  always-reject-url-rewrite = false
  private-ip-answer = true
  dns-direct-fallback-proxy = true

  [Rule]
  DOMAIN-SUFFIX,githubusercontent.com,PROXY
  RULE-SET,https://raw.githubusercontent.com/tauCross/cross_rules/main/block.list,REJECT
  RULE-SET,https://raw.githubusercontent.com/tauCross/cross_rules/main/proxy.list,PROXY
  FINAL,DIRECT

  [Host]
  localhost = 127.0.0.1

  [URL Rewrite]
  ^https?://(www.)?g.cn https://www.google.com 302
  ^https?://(www.)?google.cn https://www.google.com 302
  ```