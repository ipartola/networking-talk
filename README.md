
# Stack Model

Two models:

[OSI](http://en.wikipedia.org/wiki/OSI_model) is abstract:

![OSI Model](http://upload.wikimedia.org/wikipedia/commons/2/2b/Osi-model.png)

[TCP/IP Reference Model](http://en.wikipedia.org/wiki/TCP/IP_model) is intuitive:

![IP Stack](http://upload.wikimedia.org/wikipedia/commons/c/c4/IP_stack_connections.svg)
![UDP Encapsulation](http://upload.wikimedia.org/wikipedia/commons/3/3b/UDP_encapsulation.svg)

"We reject: kings, presidents and voting. We believe in: rough consensus and running code." ~ [David D. Clark](http://en.wikipedia.org/wiki/David_D._Clark)

# Internet Protocol

Two protocols actively in use IPv4 and IPv6. Identical in function, slightly different implementations. IP properties:

* Unreliable but simple
* "Brick with a note" model
* Addressing whole hosts

![IPv4 vs IPv6 headers](http://2.bp.blogspot.com/-y8SWF1V2YYE/TlUuuddulTI/AAAAAAAAAOM/5lWHruyWh3c/s1600/ipv4_ipv6.jpg)

IPv4 may fragment and re-assemble packets. IPv6 does away with this in favor of [MTUPD](http://en.wikipedia.org/wiki/Path_MTU_Discovery).

IP addresses may be spoofed. This is typically not an issue since routers can usually detect this.

# ICMP/ICMPv6

* Sometimes considered at IP level and sometimes above it.
* Used by hosts to communicate about the network.
* Increasingly important for IPv6.

![ICMP header](http://www.winsocketdotnetworkprogramming.com/winsock2programming/winsock2advancedrawsocket11_files/image002.png)

traceroute uses ICMP by sending packets with increasing TTL value and getting the response.

# UDP

Designed 6 years after TCP (1980). Similary to IP, but for direct use by applications:

* Unreliable but simple
* "Brick with a note" model
* Addressing applications/services

Adds the concept of "ports" (aka "service numbers", aka "AEN" - Another Eightbit Number). Individual applications/services may use well-defined ports. Source port is optional in IPv4.

![UDP Header](http://ipv6.com/images/diagrams/udp2.gif)

Some uses of UDP include:

* DNS
* VPNs/Tunnels
* Whenever reliability is not a priority
* Whenever a higher-level protocol guarantees reliability

# TCP

Reliable protocol with the goal of delivering correct data "eventually". Main features include:

* Connection-oriented communication
* Data buffering
* Reliability via positive acknowledgement
* Congestion control

![TCP Header](http://systemstechblog.files.wordpress.com/2011/02/tcpheader.jpg)

Includes lots of old-school assumptions and is optimized for slow and very unreliable networks. `TCP_NODELAY` socket option prevents unnecessary 200ms buffering.

Do not tunnel TCP in TCP: congestion control on the low level will screw with congestion control on the top level.

# HTTP

Application level protocol implemented on top of TCP. Two versions actively supported: 1.0 and 1.1. Version 1.1 resulted in widespread adoption of apache, which resulted in widespread adoption of Linux.

Text-based protocol:

``
$ telnet localhost 80
GET / HTTP/1.0
Host: localhost

HTTP/1.1 200 OK
Server: nginx/1.0.5
Date: Wed, 15 Feb 2012 16:31:54 GMT
Content-Type: text/html
Content-Length: 172
Connection: close
``

New features in HTTP/1.1:

* Connection: keep-alive and Connection: close
* Virtual hosts (apache first to provide wide-spread support)
* Better caching semantics: ETags, Cache-Control
* Vary header - modify cache key based on other headers
* Range requests: allows to resume downloads
* Compression: deflate, gzip, etc.
* Pipelining: very poorly supported
* Content negotiation using Accept-Charset, Accept-Language, etc.

Many DoS attacks possible. One such attack is Slolaris: send requests to server very slowly.

# Firewalls

A firewall is a data filter. Can operate at any level. Most operate at IP or Transport. HTTP firewalls exist.

Can filter on any combination of address/network, port, connection state. Can also provide translation: host A thinks it's talking to B when it's really talking to C.

# "Click here to read more"

* [Mobile IP]() - keeping the same address on different networks
* [IP in IP tunnelling]()
* [Multicast/Broadcast]()
* [NAT]()
* [Anycast]()
* [BGP]()
* Transports other than TCP/UDP
