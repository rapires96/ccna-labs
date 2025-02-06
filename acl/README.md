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

``` 
