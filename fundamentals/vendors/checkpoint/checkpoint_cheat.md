---
layout: default
---

## Table of Contents

- [Firewall Commands](#firewall-commands)
- [Sniffer on the Firewall](#sniffer-on-the-firewall)

## Firewall Commands

#### Show Firewall Version

```
fw ver	
```

#### Generate MAC Address for users. This can be used to fix an IP in DHCP Server.

```
vpn macutil
```

#### Show the connected and the licensed users

```
cpstat polsrv -f all
```

#### Check protocol states.

```
cpstat fw -f http, ftp, telnet, rlogin, smtp, pop3
```

#### Show policy name and the interfaces that have already seen any traffic.

```
fw stat
```

#### Shows the policy and the stats for the policy

```
fw stat -long
```

#### Monitor CPU state every 3 seconds

```
cpstat os -f cpu -o 3
```

-o Polling interval (seconds) specifies the pace of the results. Default is 0, meaning the results are shown only once.
-c Specifying how many times the results are shown. Default is 0, meaning the results are repeatedly shown.	cpstat useful parameters

#### Show SVN Foundation and OS Version

```
cpstat os
```

#### Product, Policy und Status informations

```
cpstat fw -f all
```

#### Show Installed Policy name

```
cpstat fw -f policy
```

#### Show active connections

```
fw tab -t connections -s
```

#### Install Policy from MGM server

```
fw fetch
```

#### Print licenses

```
cplic print
```

#### Connecting multiple clusters to the same network segment (same VLAN, same switch) – sk25977

```
fwha_mac_magic
```

#### SIC test on the firewall

```
cp_conf sic state
```

#### SIC reset on the firewall

```
cp_conf sic init <Activation Key> [norestart]
```

#### Check dropped packets on the firewall for host 1.1.1.1

```
fw ctl zdebug drop | grep 1.1.1.1
```

## Sniffer on the Firewall

#### Monitor traffic between host with IP IP_S and host with IP IP_D

```
fw monitor -m iIoO -e “accept (src=IP_S and dst=_IP_D) or (src=IP_D and dst=IP_S);”
```

#### Not just monitor but save as capture to a file

```
fw monitor -m iIoO -e “accept (src=IP_S and dst=_IP_D) or (src=IP_D and dst=IP_S);” -ow monitor_cat.cap”
```

#### Not just monitor but save capture to a file + deeper debug

```
fw monitor -m iIoO -e “accept (src=IP_S and dst=_IP_D) or (src=IP_D and dst=IP_S);” -p all -a -o Datei.cap
```

#### Monitor traffic on the source port 5200, 5100 or 5000

```
fw monitor -m iIoO -e “accept (sport=5200 or sport=5100 or sport=5000);”
```


[Back](/vendors/checkpoint.html)
