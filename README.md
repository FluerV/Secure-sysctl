# Secure sysctl 

1. To save changes run: 
sysctl -p

2. Reboot!

3. Check if your modification exist (with su):
#sysctl -a | grep your interface

# Explanation

0 - disable option
1 - enable option

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



