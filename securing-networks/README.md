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

