# Logging

### Setting up a syslog server for IOS swiches and routers

- Select host and logging level. In pt functionality is limited, only debugging.
```bash
logging host <syslog-ip>
logging trap debugging 
```
- Verify
```bash
show logging
```

- (Optional) setup buffered logs. In pt only defining the suze is allowed.
```bash
logging buffered <4096-2147483647>
```

- Use debug cmd to monitor specific processes
```bash
debug ip ospf hello
```

- Use carefully debug in production systems since it consumes CPU
```bash
show process cpu
```

# NTP configuration

- Configure router either as ntp server or ntp client&server. these can be done simultaneously to provide redundancy to the network
```
ntp master <1-5 stratum level> 
ntp server <ntp-server-ip>
```

- Verify,associations 
```bash
show ntp associations
show ntp status
```

- Configure a loopback interface so routers ntp service is always available
```bash
Router(config)#int loopback 0
Router(config-if)#ip address 172.16.10.100 255.255.255.0
Router(config-if)#ntp master 2
```

# CDP and LLDP
Cisco Discovery Protocol and Link Layer Discovery Protocol

```bash
show cdp neighbors
show cdp neighbors detail
show cdp entry <name of the neighbors> # Gives the detail of the neighbor
```

```bash
no cdp enable #to disable cdp in the interface
no cdp run # to disbale globally
```
- Verify
```bash
show cdp
show cdp interface <type number>
show cdp traffic
```

- LLDP, msut be first enabled in global configuration

```bash
lldp run
```

- Then find neighbor details

```bash
show lldp neighbors
```

# Configure NAT

### Static NAT

- Define the inside and outside NAT interface
```bash
ip nat inside
ip nat outside
```
- Define the IP translations in global configurations
```bash
ip nat inside source <inside-local-ip> <inside-global-ip>
```
- Verify
```bash
show ip nat translations
show ip nat statistics
```
### Dynamic NAT 

- Define inside and outside NAT interfaces (same as static)

- create a acl for the inside local addresses and add them to the inside gloabl pool
```bash
Router(config)#access-list 1 permit 172.20.1.2
Router(config)#access-list 1 permit 172.20.1.0 0.0.0.255
Router(config)#int gi0/1
Router(config-if)#ip access-group 1 in
Router(config-if)#exit
Router(config)#ip nat pool test 200.1.1.253 200.1.1.254 netmask 255.255.255.248
Router(config)#ip nat inside source list 1 pool test
```
### Dynamic NAT Overload (PAT)

- Add the overload keyword to previous dynamic NAT configurations.
```bash
access-list 1 permit 192.168.1.0 0.0.0.255
int gi0/1
ip access-group 1 in 
(config) ip nat inside source list 1 interface gi 0/1 overload #its possible to use pools also 
Router(config)#ip nat pool fred 200.1.1.251 200.1.1.254 netmask 255.255.255.248
Router(config)#ip nat inside source list 1 pool fred overload
```


