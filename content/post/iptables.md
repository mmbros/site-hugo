+++
date = "2017-11-08T09:11:00+01:00"
draft = true
title = "IPTables"
tags = ["linux", "iptables", "firewall"]

+++

### Riferimenti

* [Iptables Tutorial 1.2.2](https://www.frozentux.net/iptables-tutorial/iptables-tutorial.html) an as complete reference as possibly to iptables and netfilter
* [iptables-boilerplate](https://github.com/bmaeser/iptables-boilerplate) rock solid default firewall-rules for webhosts
* [Building a Professional Firewall with Linux and Iptables](https://danielmiessler.com/blog/professional-firewall-iptables) from Daniel Miessler blog
* [Linux IPTables: Incoming and Outgoing Rule Examples (SSH and HTTP)](http://www.thegeekstuff.com/2011/03/iptables-inbound-and-outbound-rules/)

### Configurazione di esempio

```
#!/bin/bash

IPTABLES=/sbin/iptables

SSH_PORT=22

#################################################################
# CLEAR ALL RULES
#################################################################

# delete old rules
$IPTABLES -F
# delete every non-builtin chain
$IPTABLES -X


#################################################################
# DEFAULT POLICIES
#################################################################

$IPTABLES -P INPUT DROP
$IPTABLES -P FORWARD DROP
$IPTABLES -P OUTPUT DROP


#################################################################
# ALLOW DEFAULTS
#################################################################

# allow anything on local interface
$IPTABLES -A INPUT -i lo -j ACCEPT
$IPTABLES -A OUTPUT -o lo -j ACCEPT

# allow all packets that already have a connection
$IPTABLES -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# allow ICMP
$IPTABLES -A INPUT -p icmp -j ACCEPT


#################################################################
# MANAGE SSH
#################################################################

# allow incoming SSH only from 192.168.1.XXX network.
$IPTABLES -A INPUT -i eth0 -p tcp -s 192.168.1.0/24 \
          --dport $SSH_PORT -m state --state NEW,ESTABLISHED \
		  -j ACCEPT
$IPTABLES -A OUTPUT -o eth0 -p tcp --sport $SSH_PORT \
          -m state --state ESTABLISHED -j ACCEPT

# allow outgoing SSH
$IPTABLES -A OUTPUT -o eth0 -p tcp --dport $SSH_PORT \
          -m state --state NEW,ESTABLISHED -j ACCEPT
$IPTABLES -A INPUT -i eth0 -p tcp --sport $SSH_PORT \
          -m state --state ESTABLISHED -j ACCEPT


#################################################################
# Log Dropped Packets
#################################################################

# create a new chain called LOGGING
$IPTABLES -N LOGGING

# make sure all the remaining incoming connections 
# jump to the LOGGING chain as shown below
$IPTABLES -A INPUT -j LOGGING

# log these packets by specifying a custom "log-prefix"
$IPTABLES -A LOGGING -m limit --limit 1/sec -j LOG \
          --log-prefix "MMFirewall Packet Dropped: " --log-level 7
 
# drop these packets
$IPTABLES -A LOGGING -j DROP
```
