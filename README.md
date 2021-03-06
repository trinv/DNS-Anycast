# DNS-Anycast

## Add loopback interface lo:0 for DNS Anycast IP Address:
``#cd /etc/sysconfig/network-scripts``

``#vi ifcfg-lo:0``

## Add all information in config file loopback-interface into ifcfg-lo:0

``#systemctl restart network``

## Assign IP Address of your Server's interfaces:

```Example:
- interface: eno1 for management (ifcfg-eno1)
- interface: eno2 for peering BGP to announce DNS Anycast IP/ASN (ifcfg-eno2)
--> Then you need restart network to apply new configure.
```

## Install BIRD

```
- Requirement packages:

+ GNU C Compiler (or LLVM Clang)
+ GNU Make
+ GNU Bison
+ GNU M4
+ Flex
+ ncurses library: yum install ncurses-devel
+ GNU Readline library: yum install readline-devel
+ libssh library (optional, for RPKI-Router protocol)
+ binutils
```
- Download BIRD package & extract:

``#wget https://bird.network.cz/download/bird-2.0.7.tar.gz``

``#tar -xvf bird-2.0.7.tar.gz``
- Installing:

``#cd bird-2.0.7``

``#./configure``

``#make``

``#make install``

``#bird``

- Add BIRD config: bird.conf

## Allow IPv6 & forwarding port on this DNS Anycast Server:

``#vi /etc/iproute2/rt_tables (rt_tables configure file)``

``--> Reboot the server to apply new config``

## Allow IPv6 & Forwarding port

Add some lines into /etc/sysctl.conf

``#vi /etc/sysctl.conf``

``#sysctl --system reload``

## Reboot

