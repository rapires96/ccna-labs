# VLAN, RSTP, Etherchannels and BPDU guard 

Basic Vlan configuration, set RSTP interface settings, costs and priorities, etherchannels and loadbalacing, and bpdu guard.
{vlan-rstp}[./lab2.png]

- VLAN trunk and access
```bash
switchport mode access
switchport access vlan <nbr>
#
switcport mode trunk 
switchport trunk allowed vlan <n, n+1>
```

- Etherchannels
```bash
channel-group 1 mode {on, desirable|auto, active|passive}
port-channel load-balance <src-ip, ...>
```

- RSTP priority, root bridge, port cost
```bash
spanning-tree vlan <n> root {primary|secondary}
spanning-tree vlan <n> priority <value>

(config-if) spanning-tree vlan <n> cost <x>

(config-if) spanning-tree portfast
(config-if) spanning-tree bpduguard enable
(config-if) spanning-tree link-type point-to-point
```



