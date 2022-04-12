# 以下主体摘自Clash官方配置文档，如使用TAP/TUN自行摘取，不可全搬，

## 推荐：

>* TAP模式建议使用 redir-host 模式，推荐摘取内容如下：
```
mixin:
  dns:
    enable: true
    ipv6: false
    listen: 0.0.0.0:53
    enhanced-mode: redir-host
    use-hosts: true # lookup hosts and return IP record
    fake-ip-range: 198.18.0.1/16
    nameserver:
      - 114.114.114.114 # Public DNS
      - 223.5.5.5 # AliDNS
      #- 119.29.29.29 # DNSPod
      - tls://223.5.5.5:853
      #- tls://dns.rubyfish.cn:853 # DNS over TLS
      #- dhcp://en0 # dns from dhcp
    fallback:
      - 8.8.8.8 # Google DNS
      #- tls://8.8.8.8 # Google
      #- tls://1.1.1.1 # cloudflare
      #- https://1.1.1.1/dns-query # cloudflare
    fallback-filter:
      geoip: true
      geoip-code: CN
      ip-cidr:
        - 240.0.0.0/4
        - 127.0.0.1/8
        - 0.0.0.0/32
      domain:
        - +.github.com
        - +.google.com
        - +.facebook.com
        - +.youtube.com

```     
>* TUN模式建议使用 fake-ip 模式，推荐摘取内容如下：
```
mixin:
  dns:
    enable: true
    ipv6: false
    listen: 0.0.0.0:53
    enhanced-mode: fake-ip
    use-hosts: true # lookup hosts and return IP record
    default-nameserver:
      - 114.114.114.114 # Public DNS
      - 8.8.8.8 # Google DNS
      - 119.29.29.29 # DNSPod
      - 223.5.5.5 # AliDNS
      #- 180.76.76.76 # Baidu DNS
      #- 208.67.222.222 # OpenDNS
      #- 1.0.0.1 # Cloudflare DNS
    fake-ip-range: 198.18.0.1/16 # Fake IP addresses pool CIDR
    fake-ip-filter:
      - '+.msftconnecttest.com'
      - '+.msftncsi.com'
      - '+.xboxlive.com'
      - 'msftconnecttest.com'
      - 'xbox.*.microsoft.com'
    nameserver:
      - tls://223.5.5.5:853
      #- tls://dns.rubyfish.cn:853 # DNS over TLS
      #- https://1.1.1.1/dns-query # DNS over HTTPS
      - https://doh.pub/dns-query # DNSPod
      - https://dns.alidns.com/dns-query # AliDNS
      - dhcp://en0 # dns from dhcp
    fallback:
      #- tls://185.222.222.222
      - tls://8.8.8.8 # Google
      #- tls://1.1.1.1 # cloudflare
      #- https://dns.google.com/dns-query 
      - https://cloudflare-dns.com/dns-query #Cloudflare DNS
      #- https://doh.dns.sb/dns-query #DNS.SB
      #- https://dns-unfiltered.adguard.com/dns-query #AdguardDNS
      - https://doh.opendns.com/dns-query #OpenDNS
    fallback-filter:
      geoip: true
      geoip-code: CN
      ip-cidr:
        - 240.0.0.0/4
        - 127.0.0.1/8
        - 0.0.0.0/32
      domain:
        - +.github.com
        - +.google.com
        - +.facebook.com
        - +.youtube.com
        - +.xn--ngstr-lra8j.com
        - +.google.cn
        - +.googleapis.cn
  tun:
    enable: true
    stack: gvisor # or system
    dns-hijack:
     - 198.18.0.2:53 # when `fake-ip-range` is 198.18.0.1/16, should hijack 198.18.0.2:53
     # - 8.8.8.8:53
     # - tcp://8.8.8.8:53
    auto-route: true # auto set global route for Windows
    # It is recommended to use `interface-name`
    auto-detect-interface: true # auto detect interface, conflict with `interface-name`
    
```

* 
* 
* 
# 完整内容如下，使用自摘。
```
mixin:
  dns:
    enable: true
    ipv6: false # when the false, response to AAAA questions will be empty
    listen: 0.0.0.0:53
    enhanced-mode: redir-host # or fake-ip
    use-hosts: true # lookup hosts and return IP record
    
    # These nameservers are used to resolve the DNS nameserver hostnames below.
    default-nameserver:
      - 114.114.114.114 # Public DNS
      - 8.8.8.8 # Google DNS
      - 119.29.29.29 # DNSPod
      - 223.5.5.5 # AliDNS
      #- 180.76.76.76 # Baidu DNS
      #- 208.67.222.222 # OpenDNS
      #- 1.0.0.1 # Cloudflare DNS

    fake-ip-range: 198.18.0.1/16 # Fake IP addresses pool CIDR
    # Hostnames in this list will not be resolved with fake IPs
    # i.e. questions to these domain names will always be answered with their real IP addresses
    # 当enhanced-mode设置为fake-ip时，会出现系统检测到网卡无法联网，
    # 微软系 APP 无法登陆使用等问题，可以通过添加fake-ip-filter解决：
    #fake-ip-filter:
       #- '*.lan'
       #- localhost.ptlogin2.qq.com
       #- '+.srv.nintendo.net'
       #- '+.stun.playstation.net'
       #- '+.msftconnecttest.com'
       #- '+.msftncsi.com'
       #- '+.xboxlive.com'
       #- 'msftconnecttest.com'
       #- 'xbox.*.microsoft.com'
       #- '*.battlenet.com.cn'
       #- '*.battlenet.com'
       #- '*.blzstatic.cn'
       #- '*.battle.net'

    # Supports UDP, TCP, DoT, DoH. You can specify the port to connect to.
    # All DNS questions are sent directly to the nameserver, without proxies
    # involved. Clash answers the DNS question with the first result gathered.
    nameserver:
      - tls://223.5.5.5:853
      - tls://dns.rubyfish.cn:853 # DNS over TLS
      #- https://1.1.1.1/dns-query # DNS over HTTPS
      - https://doh.pub/dns-query # DNSPod
      - https://dns.alidns.com/dns-query # AliDNS
      - dhcp://en0 # dns from dhcp

    # When `fallback` is present, the DNS server will send concurrent requests
    # to the servers in this section along with servers in `nameservers`.
    # The answers from fallback servers are used when the GEOIP country is not `CN`.
    # if https-dns not working,try (DOT)tls://
    #fallback:
      #- tls://185.222.222.222
      #- tls://8.8.8.8 # Google
      #- tls://1.1.1.1 # cloudflare
      #- https://1.1.1.1/dns-query # cloudflare
      #- https://cloudflare-dns.com/dns-query #Cloudflare DNS
      #- https://freedns.controld.com/p0 #Control DNS
      #- https://doh.dns.sb/dns-query #DNS.SB
      #- https://dns-unfiltered.adguard.com/dns-query #AdguardDNS
      #- https://doh.opendns.com/dns-query #OpenDNS
      #- https://private.canadianshield.cira.ca/dns-query #CIRADNS
      #- https://dns.nextdns.io #NextDNS, you can sign up to get your own
      #- https://dns.quad9.net:5053/dns-query #Qua9DNS
      #- https://dns.twnic.tw/dns-query #台灣網路資訊中心 DNS
    
    # If IP addresses resolved with servers in `nameservers` are in the specified
    # subnets below, they are considered invalid and results from `fallback`
    # servers are used instead.
    #
    # IP address resolved with servers in `nameserver` is used when
    # `fallback-filter.geoip` is true and when GEOIP of the IP address is `CN`.
    #
    # If `fallback-filter.geoip` is false, results from `nameserver` nameservers
    # are always used if not match `fallback-filter.ipcidr`.
    #
    # This is a countermeasure against DNS pollution attacks.
    fallback-filter:
      geoip: true
      geoip-code: CN
      ip-cidr:
        - 240.0.0.0/4
        - 127.0.0.1/8
        - 0.0.0.0/32
      domain:
        - +.github.com
        - +.google.com
        - +.facebook.com
        - +.youtube.com
        - +.xn--ngstr-lra8j.com
        - +.google.cn
        - +.googleapis.cn


    # Lookup domains via specific nameservers
    # nameserver-policy:
    #   'www.baidu.com': '114.114.114.114'
    #   '+.internal.crop.com': '10.0.0.1'

  tun:
    enable: true
    stack: gvisor # or system
    dns-hijack:
     - 198.18.0.2:53 # when `fake-ip-range` is 198.18.0.1/16, should hijack 198.18.0.2:53
     # - 8.8.8.8:53
     # - tcp://8.8.8.8:53
    auto-route: true # auto set global route for Windows
    # It is recommended to use `interface-name`
    auto-detect-interface: true # auto detect interface, conflict with `interface-name`
    
```
    
    
