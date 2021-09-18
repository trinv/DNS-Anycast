# DNS-Anycast
1. Add loopback interface lo:0 for DNS Anycast IP Address:
#cd /etc/sysconfig/network-scripts
#vi ifcfg-lo:0
Add all information in config file loopback-interface into ifcfg-lo:0
#systemctl restart network

2. Assign IP Address of your Server's interfaces:

Example:
- interface: eno1 for management (ifcfg-eno1)
- interface: eno2 for peering BGP to announce DNS Anycast IP/ASN (ifcfg-eno2)
--> Then you need restart network to apply new configure.

3. Install BIRD

- Requirement packages:

+ GNU C Compiler (or LLVM Clang)
+ GNU Make
+ GNU Bison
+ GNU M4
+ Flex
+ ncurses library
+ GNU Readline library
+ libssh library (optional, for RPKI-Router protocol)
+ binutils
- Download BIRD package & extract:

# wget https://bird.network.cz/download/bird-2.0.7.tar.gz
# tar -xvf bird-2.0.7.tar.gz
- Installing:

# cd bird-2.0.7
# ./configure
# make
# make install
# bird
- Add BIRD config: bird.conf

4. Allow IPv6 & forwarding port on this DNS Anycast Server:

# vi /etc/iproute2/rt_tables (rt_tables configure file)
--> Reboot the server to apply new config
5. Allow IPv6 & Forwarding port
Add some lines into /etc/sysctl.conf
#vi /etc/sysctl.conf
net.ipv4.conf.default.forwarding = 1
net.ipv6.conf.default.autoconf = 1
net.ipv6.conf.all.forwarding = 1
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.autoconf = 1
net.ipv6.conf.default.forwarding = 1
net.ipv6.conf.default.diable_ipv6 = 0
net.ipv6.conf.all.accept_ra = 1
net.ipv6.conf.default.accept_ra = 1

6. Reboot
