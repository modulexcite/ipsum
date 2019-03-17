![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

**Important:** If you are planning to use `git` to get the content of this repository do it like `git clone --depth 1 https://github.com/stamparm/ipsum.git`

Wall of shame (2019-03-17)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
171.25.193.20|tor-exit0-readme.dfri.se|11
171.25.193.25|tor-exit5-readme.dfri.se|10
171.25.193.77|tor-exit1-readme.dfri.se|10
128.31.0.13|tor-exit.csail.mit.edu|9
89.234.157.254|marylou.nos-oignons.net|9
197.231.221.211|exit1.ipredator.se|9
65.19.167.131|-|9
185.220.101.46|-|9
185.220.101.33|-|9
185.220.102.4|-|8
125.64.94.200|-|8
37.220.36.240|-|8
51.77.177.194|ip194.ip-51-77-177.eu|8
42.61.24.202|-|8
171.25.193.78|tor-exit4-readme.dfri.se|8
209.95.51.11|nyc-exit.privateinternetaccess.com|8
31.220.0.225|exit3.tor-network.net|8
185.220.101.45|-|8
185.53.88.82|-|8
18.85.192.253|wholesomeserver.media.mit.edu|8
185.220.101.15|-|8
192.160.102.170|ogopogo.relay.coldhak.com|8
185.220.101.27|-|8
185.220.101.22|-|8
122.2.223.242|122.2.223.242.static.pldt.net|8
