# Secure-sysctl


#
# /etc/sysctl.conf - Configuration file for setting system variables
# See /etc/sysctl.d/ for additonal system variables
# See sysctl.conf (5) for information.
#


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

net.ipv4.conf.all.rp_filter=1

net.ipv4.conf.lo.rp_filter=1

net.ipv4.conf.wlo1.rp_filter=1

net.ipv4.conf.default.rp_filter=1
#
#Uncomment the next line to enable TCP/IP SYN cookies
#See http://lwn.net/Articles/277146/
#Note: This may impact IPv6 TCP sessions too

net.ipv4.tcp_syncookies=1
#
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

net.ipv4.conf.lo.forwarding=0

net.ipv4.conf.wlo1.forwarding=0

net.ipv4.conf.default.forwarding=0

#net.ipv6.conf.all.forwarding=0

net.ipv4.conf.all.mc_forwarding=0

net.ipv4.conf.lo.mc_forwarding=0

net.ipv4.conf.wlo1.mc_forwarding=0

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

net.ipv4.conf.all.accept_redirects = 0

net.ipv4.conf.lo.accept_redirects = 0

net.ipv4.conf.wlo1.accept_redirects = 0

#net.ipv6.conf.all.accept_redirects = 0

net.ipv4.conf.default.accept_redirects = 0

#_or_
#Accept ICMP redirects only for gateways listed in our default
#gateway list (enabled by default)

net.ipv4.conf.all.secure_redirects = 0

net.ipv4.conf.lo.secure_redirects = 0

net.ipv4.conf.wlo1.secure_redirects = 0

net.ipv4.conf.default.secure_redirects = 0

#net.ipv6.conf.all.secure_redirects = 0
#
#Do not send ICMP redirects (we are not a router)

net.ipv4.conf.all.send_redirects = 0

net.ipv4.conf.lo.send_redirects = 0

net.ipv4.conf.wlo1.send_redirects = 0

net.ipv4.conf.default.send_redirects = 0

#net.ipv6.conf.all.send_redirects = 0
#
#Do not accept IP source route packets (we are not a router)

net.ipv4.conf.all.accept_source_route = 0

net.ipv4.conf.lo.accept_source_route = 0

net.ipv4.conf.wlo1.accept_source_route = 0

net.ipv4.conf.default.accept_source_route = 0

#net.ipv6.conf.all.accept_source_route = 0
#

net.ipv4.conf.all.shared_media = 0

net.ipv4.conf.lo.shared_media = 0

net.ipv4.conf.wlo1.shared_media = 0

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

#
To save changes run: 
sysctl -p

Reboot!

Check if your modification exist:

#sysctl -a | grep your interface
#
Disable IPv6 in grub:

GRUB_CMDLINE_LINUX_DEFAULT="quiet splash ipv6.disable=1"

After making changes in grub run 

#update-grub
#
Explanation

0 - disable option

1 - enable option
#
# Ignoring broadcast request.

If your host is spoofed, attacker can send large ammounts of ICMP broadcast messages to other hosts. All hosts receiving this message will
start to reply  to your compromised address. It can significantly reduce the speed of internet connection and increase traffic.
Your computer can freeze and start working very slowly. 

# Disable packet forwarding

If your computer are not a router (gateway) between LAN nodes and your ISP you should skip forwarding. 

# Turn on Source Address Verification

It is your first network-related security task. When an IP packet is sent from a host, the routers should check to make shure that 
the packet carries a legally assigned source IP address. If this access network source address validation is missing, then a host may be able to spoof
the source IP address which belogns to another local host. 

# Disable ICMP redirects

When hosts use a non-optimal or defunct route to a particular destination, an ICMP redirect packet is used by routers to inform the hosts what the correct route should be. If an attacker is able to forge ICMP redirect packets, he or she can alter the routing tables on the host and possibly subvert the security of the host by causing traffic to flow via a path you didn't intend. It's strongly recommended to disable ICMP Redirect Acceptance to protect your server from this hole. 

The Internet Control Message Protocol (ICMP) is a supporting protocol in the Internet protocol suite. 
It is used by network devices, including routers, to send error messages, for example, an error is indicated when a requested service is not available or that a host or router could not be reached.

# Do not send ICMP redirects

The ICMP Redirect message is used to notify a remote host to send data packets on an alternative route. 
A host SHOULD NOT send an ICMP Redirect message. Redirects SHOULD only be sent by gateways.

# Do not accept IP source route packets

Source routing is a technique whereby the sender of a packet can specify the route that a packet should take through the network.
As a packet travels through the network, each router will examine the destination IP address and choose the next hop to forward the packet to. 
In source routing, the "source" (i.e., the sender) makes some or all of these decisions.

Reason for disabling: Attackers can use source routing to probe the network by forcing packets into specific parts of the network. Using source routing, an attacker can collect information about a network's topology, or other information that could be useful in performing an attack. 
During an attack, an attacker could use source routing to direct packets to bypass existing security restrictions.

# Disable shared media

The shared_media setting tells the kernel if the physical network connected to a specific network card is a shared media or not. 
For example, if several different IP networks with different netmasks operate over the same physical media or not. 
The main effect that this variable makes, is to tell the kernel whether it should send ICMP redirects to specific networks or not.

Per default this variable is turned on. It takes a boolean value, and may hence be turned on or off. Note that this variable overrides secure_redirects below. 

# Enable TCP/IP SYN cookies

The attacker begin with the TCP connection handshake sending the SYN packet, and then never completing the process to open the connection. 
This results into massive half-open connections. The Linux kernel can block such attacks easily. Enable TCP/IP SYN cookies for that task. 



