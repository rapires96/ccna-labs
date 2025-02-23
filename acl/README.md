# Configure Access Control Lists in terminals

### Standard numbered ACL (1-99, 1300-1999)

```bash
# configure terminal
(config) # access-list 1 permit 10.1.1.1
(config) # access-list 1 deny 10.1.1.0 0.0.0.255
(config) # access-list 1 permit 10.0.0.0 0.255.255.255
(config) # access-list 1 deny any # this is the default behaviour of ACLs not needed
(config) # interface gi0/1
(config-if) # ip access-group 1 in
(config-if) # ^Z
# show running-config
# show ip access-list 1
# show ip interface gi0/1
```

### Extended numbered ACL (101-199, 2000-2699) 

```bash
(config)#access-list 101 deny tcp host 192.168.11.2 192.168.10.0 0.0.0.255 eq ftp
(config)#access-list 101 deny tcp host 192.168.12.2 host 192.168.10.3 eq www
(config)#access-list 101 permit ip any any
(config)#int gi0/0
(config-if)#ip access-group 101 in
(config-if)#int gi0/1
(config-if)#ip access-group 101 in
(config-if)#
```

### Named ACLs

```bash
Router(config)#ip access-list extended alburquerque
Router(config-ext-nacl)#deny ip host 172.20.10.3 host 172.20.11.2
Router(config-ext-nacl)#deny ip host 172.20.12.3 172.20.10.0 0.0.0.255
Router(config-ext-nacl)#deny ip host 172.20.10.2 172.20.12.0 0.0.0.255
Router(config-ext-nacl)#permit ip any any
Router(config-ext-nacl)#int gi 0/2
Router(config-if)#ip access-group alburquerque in
Router(config-if)#int gi 0/1
Router(config-if)#ip access-group alburquerque in
Router(config-if)#int gi 0/0
Router(config-if)#ip access-group alburquerque in
```


```bash
Router#show ip access-list
Extended IP access list alburquerque
    10 deny ip host 172.20.10.3 host 172.20.11.2
    20 deny ip host 172.20.12.3 172.20.10.0 0.0.0.255
    30 deny ip host 172.20.10.2 172.20.12.0 0.0.0.255
    40 permit ip any any

Router#
Router#
Router#
Router#ip access-list extended alburquerque
          ^
% Invalid input detected at '^' marker.
	
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#ip access-list extended alburquerq
Router(config)#ip access-list extended alburquerque
Router(config-ext-nacl)#no 40
Router(config-ext-nacl)#exit
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console

Router#show ip access-list
Extended IP access list alburquerque
    10 deny ip host 172.20.10.3 host 172.20.11.2
    20 deny ip host 172.20.12.3 172.20.10.0 0.0.0.255
    30 deny ip host 172.20.10.2 172.20.12.0 0.0.0.255

Router#
```
