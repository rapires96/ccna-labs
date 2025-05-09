# IPv6 and Routing Basics

[]{./testnet.png}

The lab has been configured with various types of IPv6 addresses (Link Local, and Global Unicast) and router's configuration shows the different types of static routes.

```bash
ipv6 unicast-routing
# When defining static routes with link local addresses both outgoing interface and destination addresses are needed
ipv6 route 2001:DB8:1111:1::/64 S0/0/1 fe80:ff::fe00:1

# Defining a floating static route (with cost for the routing table)
ipv6 route 2001:db8:1111:1::/64 2001:db8:1111:9::5 130
```

A simple way of defining IPv6 addresses on intefaces is using EUI 64

```bash
ipv6 address 2001:db8:1111:1::/64 eui64
```
