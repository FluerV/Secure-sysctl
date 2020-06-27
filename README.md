# Secure-sysctl

#
#/etc/sysctl.conf - Configuration file for setting system variables
#See /etc/sysctl.d/ for additional system variables.
#See sysctl.conf (5) for information.
#kernel.domainname = example.com
#Uncomment the following to stop low-level messages on console
#kernel.printk = 3 4 1 3
#Functions previously found in netbase
#Uncomment the next two lines to enable Spoof protection (reverse-path filter)
#Turn on Source Address Verification in all interfaces to
#prevent some spoofing attacks

net.ipv4.conf.lo.rp_filter=1

net.ipv4.conf.all.rp_filter=1

net.ipv4.conf.default.rp_filter=1
#
#Uncomment the next line to enable TCP/IP SYN cookies
#See http://lwn.net/Articles/277146/
#Note: This may impact IPv6 TCP sessions too
#net.ipv4.tcp_syncookies=1
#Enable ignoring broadcast request

net.ipv4.icmp_echo_ignore_broadcasts = 1

#net.ipv6.icmp_echo_ignore_broadcasts = 1

#
#Enable bad error message Protection   
#net.ipv4.icmp_ignore_bogus_error_responses = 1
#
#Uncomment the next line to enable packet forwarding for IPv4
#Enabling this option disables Stateless Address Autoconfiguration
#based on Router Advertisements for this host

net.ipv4.conf.all.forwarding=0

net.ipv4.conf.default.forwarding=0

#net.ipv6.conf.all.forwarding=0

net.ipv4.conf.all.mc_forwarding=0

net.ipv4.conf.default.mc_forwarding=0

#net.ipv6.conf.all.mc_forwarding=0
#
###################################################################
#Additional settings - these settings can improve the network
#security of the host and prevent against some network attacks
#including spoofing attacks and man in the middle attacks through
#redirection. Some network environments, however, require that these
#settings are disabled so review and enable them as needed.
#
#Do not accept ICMP redirects (prevent MITM attacks)

net.ipv4.conf.lo.accept_redirects = 0

net.ipv4.conf.all.accept_redirects = 0

#net.ipv6.conf.all.accept_redirects = 0

net.ipv4.conf.default.accept_redirects = 0

#_or_
#Accept ICMP redirects only for gateways listed in our default
#gateway list (enabled by default)

net.ipv4.conf.lo.secure_redirects = 0

net.ipv4.conf.all.secure_redirects = 0

net.ipv4.conf.default.secure_redirects = 0

#net.ipv6.conf.all.secure_redirects = 0
#
#Do not send ICMP redirects (we are not a router)

net.ipv4.conf.lo.send_redirects = 0

net.ipv4.conf.all.send_redirects = 0

net.ipv4.conf.default.send_redirects = 0

#net.ipv6.conf.all.send_redirects = 0
#
#Do not accept IP source route packets (we are not a router)

net.ipv4.conf.lo.accept_source_route = 0

net.ipv4.conf.all.accept_source_route = 0

net.ipv4.conf.default.accept_source_route = 0

#net.ipv6.conf.all.accept_source_route = 0
#
net.ipv4.conf.lo.shared_media = 0

net.ipv4.conf.all.shared_media = 0

net.ipv4.conf.default.shared_media = 0

#net.ipv6.conf.all.shared_media = 0
#
#Log Martian Packets
#net.ipv4.conf.all.log_martians = 1
#
#Magic system request Key
#0=disable, 1=enable all, >1 bitmask of sysrq functions
#See https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html
#for what other values do
#kernel.sysrq=0


To save changes run: 
sysctl -p

Reboot!

Check if your modification exist:
sysctl -a | grep your interface


Explanation

0 - disable option
1 - enable option

1.Ignoring broadcast request.

If your host is spoofed, attacker can send large ammounts of ICMP broadcast messages to other hosts. All hosts receiving this message will
start to reply  to your compromised address. It can significantly reduce the speed of internet connection and increase traffic.
Your computer can freeze and start working very slowly. 

2.Disable packet forwarding

If your computer are not a router (gateway) between LAN nodes and your ISP you should skip forwarding. 

3.Disable ICMP redirects



