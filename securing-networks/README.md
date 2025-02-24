# Securing Network Devices

On Router 0:

```bash
Router(config)#enable secret changemelater #This is a MD5 hashed password
Router#show running-config | include enable secret
enable secret 5 $1$mERr$ScnDKn4cZXoIF19W.slJ7.
Router(config)#no enable secret # removes the need for password auth to go to enable mode
```

MD5 is old and IOS includes SHA-256
```bash
enable algorithm-type sha256 secret changemelater
enable algorithm-type scrypt secret changemelater
```

On Router 1

```bash
username myname algorithm-type sha256 secret changemelater

line vty 0 4
access-class 3 in

(configure)# access-lsit 3 permit 10.1.1.0 0.0.0.255 # only allows login consoles from that network
```

## Switchport Security 
From chapter 6 

- Preconfigure the vlans and router sub interfaces, router 0 example:
```bash 
Router(config)#int gi0/1.1
Router(config-subif)#encapsulation dot1q 1 native
Router(config-subif)#ip address 10.1.1.1 255.255.255.0
Router(config-subif)#no shutdown
Router(config-subif)#int gi0/1.2
Router(config-subif)#encapsulation dot1q 2
Router(config-subif)#ip address 10.1.2.1 255.255.255.0
Router(config-subif)#no shutdown
```
- Preconfigure vlans in switches:

```bash
Switch(config)#vlan 2
Switch(config-vlan)#name server-vlan
Switch(config-vlan)#exit
Switch(config)#int fa0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 2
Switch(config-if)#int gi0/2
Switch(config-if)#switchport mode trunk
```

#### Implementing switchport security:

1. Known source MAC address:
```bash
Switch(config-if)#int fa0/1
Switch(config-if)#switchport port-security 
Switch(config-if)#switchport port-security mac-address 00D0.BC4D.D622
```
2. Sticky learn dinamically learned MAC addresses
```bash
Switch(config-if)#int gi0/2
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security mac-address sticky
```

3. Maximum 1 source addresses
```bash
Switch(config)#int gi0/2
Switch(config-if)#int fa0/1
Switch(config-if)#switchport port-
Switch(config-if)#switchport port-security maximum 1
```

#### Verifying switchport security

```bash
Switch>enable
Switch#show port-security int fa0/1
Switch#show mac address-table secure
Switch#show mac address-table static
Switch#show mac address-table dynamic
```

#### Switchport security violations

```bash
switchport port-security violation {protect|restrict|shutdown}
```

- for shutdown:
```
errdisable recovery cause psecure-violation
errrdisable recovery interval <seconds>
```

- for remote connections to switch
```bash
Switch(config)#int vlan 1
Switch(config-if)#ip address 10.1.1.100 255.255.255.0 # or use ip address dhcp
Switch(config-if)#no shutdown
```
