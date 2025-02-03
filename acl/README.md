# Configure Access Control Lists in terminals

```bash
# configure terminal
(config) # access-list 1 permit 10.1.1.1
(config) # access-list 1 deny 10.1.1.0 0.0.0.255
(config) # access-list 1 permit 10.0.0.0 0.255.255.255
(config) # interface gi0/1
(config-if) # ip access-group 1 in
(config-if) # ^Z
# show running-config
# show ip access-list 1
#show ip interface gi0/1
```

