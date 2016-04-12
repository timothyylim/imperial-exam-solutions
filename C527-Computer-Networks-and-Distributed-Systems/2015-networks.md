# 1

a.

What Are The Advantages Of IMAP?

IMAP was created to allow remote access to emails stored on a remote server. The idea was to allow multiple clients or users to manage the same inbox. So whether you log in from your home or your work computer, you will always see the same emails and folder structure since they are stored on the server and all changes you make to local copies are immediately synced to the server.

As a result, IMAP has the following advantages:

 - Mail stored on remote server, i.e. accessible from multiple different locations
 - Internet connection needed to access mail
 - Faster overview as only headers are downloaded until content is explicitly requested
 - Mail is automatically backed up if server is managed properly
 - Saves local storage space
 - Option to store mail locally

Extra information:

Choose POP If…

 - you want to access your mail from only one single device
 - you need constant access to your email, regardless of internet availability
 - your server storage space is limited

Choose IMAP If…

 - you want to access your email from multiple different devices
 - you have a reliable and constant internet connection
 - you want to receive a quick overview of new emails or emails on the server
 - your local storage space is limited
 - you are worried about backing up



http://www.makeuseof.com/tag/pop-vs-imap/

---

b.


Circuit 

- Fixed bandwidth
- Unused bandwidth wasted
- Call set-up required
- Congestion may occur at call set-up (arrival rate = transmission rate)
- Overhead on call setup only
- In-order delivery
- Circuit fails if any link or switch fails

Packet Switching

- Variable bandwidth
- Uses only bandwidth required
- No call set-up
- Congestion may occur on any packet (causing delay and reordering)
- Overhead on every packet
- Out-of-order delivery
- New route found if any link or switch fails (some data
may be lost)


---

c.

The domain system is not really needed for the world wide web per se, since users could simply type in the IP address of the server they wish to visit. It does, however, make the navigation of the world wide web significantly easier since humans are better at remembering names as opposed to strings of digits.

The difference in the time takent to process queries to a domain may be the result of caching done by a server.

http://dyn.com/blog/dns-why-its-important-how-it-works/

An interesting discussion on Stack Exchange:

http://superuser.com/questions/22470/can-the-internet-work-without-dns/22472


---

d. 

This is one of my favorite questions. UDP is so misunderstood.

In situations where your really want to get a simple answer to another server quickly, UDP works best. In general, you want the answer to be in one response packet, and you are prepared to implement your own protocol for reliability or resends. DNS is the perfect description of this use case. The costs of connection setups are way to high (yet, DNS does support a TCP mode as well).

Another case is when you are delivering data that can be lost because newer data coming in will replace that previous data/state. Weather data, video streaming, a stock quotation service (not used for actual trading), or gaming data come to mind.

Another case is when you are managing a tremendous amount of state and you want to avoid using TCP because the OS cannot handle that many sessions. This is a rare case today. In fact, there are now user-land TCP stacks that can be used so that the application writer may have finer grained control over the resources needed for that TCP state. Prior to 2003, UDP was really the only game in town.

One other case is for multicast traffic. UDP can be multicasted to multiple hosts whereas TCP cannot do this at all.

http://stackoverflow.com/questions/1099672/when-is-it-appropriate-to-use-udp-instead-of-tcp


---

e.

TCP in networks with high packet loss rates suffers from throughput penalties, since TCP regards packet losses as signals of network congestion; TCP then reduces the data transmission rate whenever the protocol detects packet losses, even though they may occur as a result of the link errors that are usual in wireless networks. 

http://www.sciencedirect.com/science/article/pii/S1389128609002060



"Reliable" does not mean the same thing for everyone. Reliable for TCP means that if you use it on lossy networks or on networks that corrupts and/or reorder packets, then you will not get garbled data, and will essentially receive good data at the end.

The problem is that TCP sucks, and while it works in these cases, it's just horribly slow. So when you use raw TCP on links that regularly loose 0.5% of packets, you will get much less performance than the theoretical data rate of (link_data_rate / (1 - packet loss rate)) on a single link, because of the TCP assumption that all packet loss are caused by congestion.

TCP was designed for networks that seldom loose packets, so TCP only has to tolerate packet loss.

One of the tasks of the reliable link thing on layer two is mainly here to compensate for TCP suckiness. They aren't supposed to be 100% reliable like TCP. For example, 802.11 accept to loose packet if the retransmission count get above a certain threshold, whereas TCP doesn't and will retransmit forever until the application or user decides that it is enough.

The reliable link thing on layer 2 is mainly there for speed. For example, on 802.11, the ack mechanism is also used by nodes so that they can decrease the modulation speed if the wireless link degrades. When 802.11 can't do ACK (e.g. for multicast frames), it typically uses the lowest modulation rate, which is often 1 Mb/s, to get maximum reliability, at the huge expense of speed.

Sometimes, when you have a network with many highly unreliable links, you may need layer 2 reliability, otherwise the whole path may have many unreliable links and the path packet loss rate might get too high to be useful. But this is often not the case on your typical networks.

Historically, TCP picked up because it allowed routers to loose packets. So routers were simpler, faster and the global result was that handling reliability on the endpoints had better performance than handling it in the core network.

http://superuser.com/questions/401935/difference-between-the-reliable-delivery-by-link-protocols-and-by-tcp


# 2

a.

Network links can be divided into two categories: those using point-to-point connections and those using broadcast channels. In any broadcast network, the key issue is how to determine who gets to use the channel when there is competition for it.

The protocols used to determine who goes next on a multiaccess channel be- long to a sublayer of the data link layer called the MAC (Medium Access Con- trol) sublayer. 

Ch4 Tanenbaum

---

b.

CSMA CA vs CSMA CD

Carrier Sense Multiple Access or CSMA is a Media Access Control (MAC) protocol that is used to control the flow of data in a transmission media so that packets do not get lost and data integrity is maintained. There are two modifications to CSMA, the CSMA CD (Collision Detection) and CSMA CA (Collision Avoidance), each having its own strengths.

CSMA operates by sensing the state of the medium in order to prevent or recover from a collision. A collision happens when two transmitters transmit at the same time. The data gets scrambled, and the receivers would not be able to discern one from the other thereby causing the information to get lost. The lost information needs to be resent so that the receiver will get it.

CSMA CD operates by detecting the occurrence of a collision. Once a collision is detected, CSMA CD immediately terminates the transmission so that the transmitter does not have to waste a lot of time in continuing. The last information can be retransmitted. In comparison, CSMA CA does not deal with the recovery after a collision. What it does is to check whether the medium is in use. If it is busy, then the transmitter waits until it is idle before it starts transmitting. This effectively minimizes the possibility of collisions and makes more efficient use of the medium.

Another difference between CSMA CD and CSMA CA is where they are typically used. CSMA CD is used mostly in wired installations because it is possible to detect whether a collision has occurred. With wireless installations, it is not possible for the transmitter to detect whether a collision has occurred or not. That is why wireless installations often use CSMA CA instead of CSMA CD.

1. CSMA CD takes effect after a collision while CSMA CA takes effect before a collision.
2. CSMA CA reduces the possibility of a collision while CSMA CD only minimizes the recovery time.
3. CSMA CD is typically used in wired networks while CSMA CA is used in wireless networks.


Read more: Difference Between CSMA CA and CSMA CD | Difference Between | CSMA CA vs CSMA CD http://www.differencebetween.net/technology/protocols-formats/difference-between-csma-ca-and-csma-cd/#ixzz441MohWgH

---

c.

no idea

---

d.

**HTTP**
Short for HyperText Transfer Protocol, HTTP is the underlying protocol used by the World Wide Web. HTTP defines how messages are formatted and transmitted, and what actions Web servers and browsers should take in response to various commands. For example, when you enter a URL in your browser, this actually sends an HTTP command to the Web server directing it to fetch and transmit the requested Web page.

HTTP is part of the application layer.

**Network Switch**

A network switch (also called switching hub, bridging hub, officially MAC bridge[1]) is a computer networking device that connects devices together on a computer network, by using packet switching to receive, process and forward data to the destination device. Unlike less advanced network hubs, a network switch forwards data only to one or multiple devices that need to receive it, rather than broadcasting the same data out of each of its ports.[2]

https://en.wikipedia.org/wiki/Network_switch

A Network Switch would exist in the link layer.

**Subnet**

A subnetwork, or subnet, is a logical, visible subdivision of an IP network.

Subnets are smaller networks that form connection – Subnets segment traffic
 - Limit propagation of signals
 
Support for underlying networks
- With different physical technologies
- With different administrative ownerships

Subnets would exist in the Internet layer.

**ARP**

The Address Resolution Protocol (ARP) is a telecommunication protocol used for resolution of network layer addresses into link layer addresses, a critical function in multiple-access networks.

Although every machine on the Internet has one or more IP addresses, these addresses are not sufficient for sending packets. Data link layer NICs (Network Interface Cards) such as Ethernet cards do not understand Internet addresses. In the case of Ethernet, every NIC ever manufactured comes equipped with a unique 48-bit Ethernet address. Manufacturers of Ethernet NICs request a block of Ethernet addresses from IEEE to ensure that no two NICs have the same address (to avoid conflicts should the two NICs ever appear on the same LAN). 

Tanenbaum 468

The ARP would exist in the Link layer. 



# 3

a.

Security for information resources has three components:
confidentiality (protection against disclosure to unauthorized individuals), integrity
(protection against alteration or corruption), and availability (protection against
interference with the means to access the resources).


---

b.

**IP packet filtering**: This is a filter process examining individual IP packets. It may make decisions based on the destination and source addresses. It may also examine the service type field of IP packets and interpret the contents of the packets based on the type. For example, it may filter TCP packets based on the port number to which they are addressed, and since services are generally located at well-known ports, this enables packets to be filtered based on the service requested. For example, many sites prohibit the use of NFS servers by external clients.
For performance reasons, IP filtering is usually performed by a process within the operating system kernel of a router. If multiple firewalls are used, the first may mark certain packets for more exhaustive examination by a later firewall, allowing ‘clean’ packets to proceed. It is possible to filter based on sequences of IP packets, for example, to prevent access to an FTP server before a login has been performed.


**TCP gateway**: A TCP gateway process checks all TCP connection requests and segment transmissions. When a TCP gateway process is installed, the setting up of TCP connections can be controlled and TCP segments can be checked for correctness (some denial of service attacks use malformed TCP segments to disrupt client operating systems). When desired, they can be routed through an application-level gateway for content checking.


**Application-level gateway**: An application-level gateway process acts as a proxy for an application process. For example, a policy may be desired that allows certain internal users to make Telnet connections to certain external hosts. When a user runs a Telnet program on their local computer, it attempts to establish a TCP connection with a remote host. The request is intercepted by the TCP gateway. The TCP gateway starts a Telnet proxy process and the original TCP connection is routed to it. If the proxy approves the Telnet operation (i.e., if the user is authorized to use the requested host) it establishes another connection to the requested host and relays all of the TCP packets in both directions. A similar proxy process would run on behalf of each Telnet client, and similar proxies might be employed for FTP and other services.

Colouris 124

---

c.



# 4

a.

 A security manager is not necessary when using RMI in Java. To understand why this is the case let's look at what a security manager does:
 
 The job of a security manager is to prevent any nasty surprises from remotely loaded classes. Therefore, you only need to install a security manager for RMI if the peer is using the codebase facility to supply classes to you dynamically.

The checks a security manager does (just imagine him as some fat security guard) is the access to
- communications
- files
- control of the virtual machine

 In RMI applications, if no security manager is set, stubs and classes can only be loaded from local classpath, so yes, you can survive without a security manager. Living without the security manager is either unecessarily risky or completely fine depending where you are loading your stubs from. 

---

lecture slides

b.

Both RPC and RMI try and solve the problem of getting executing code on a remote machine. To figure out the difference between the two it helps to understand what the bloody acronyms mean. RPC => remote procedure call, RMI => remote method invocation. To call a procedure remotely means to ask a routine to run remotely. Since methods are associated with objects, we can deduce that RMI based on object-oriented programming. 

The benefits of RMI over RPC are closely associated with the benefits of using object: i.e. you can do more complicated shit at an overhead cost. 

Three advantages:
- transparency (in terms of location and access)
 - access transparency: emote invocations should be made 
transparent in the sense that syntax of a remote 
invocation is the same as the syntax of local invocation 
 - location transparency:In a distributed system it is the idea that the resources accessed by a user can be anywhere on the network without the user having any idea where the resource is located. A file could be on the user's own PC, or thousands of miles away on another server, for example. The user would access it in the same way. 
- type checking => fewer errors
- write once, write everywhere
 - due to inheritance based structure of OOP 

RPC is C based, and as such it has structured programming semantics, on the other side, RMI is a Java based technology and it's object oriented.

With RPC you can just call remote functions exported into a server, in RMI you can have references to remote objects and invoke their methods, and also pass and return more remote object references that can be distributed among many JVM instances, so it's much more powerful.

RMI stands out when the need to develop something more complex than a pure client-server architecture arises. It's very easy to spread out objects over a network enabling all the clients to communicate without having to stablish individual connections explicitly.



1. Approach:

RMI uses an object-oriented paradigm where the user needs to know the object and the method of the object he needs to invoke.

RPC doesn't deal with objects. Rather, it calls specific subroutines that are already established.

2. Working:

With RPC, you get a procedure call that looks pretty much like a local call. RPC handles the complexities involved with passing the call from local to the remote computer.

RMI does the very same thing, but RMI passes a reference to the object and the method that is being called.

RMI = RPC + Object-orientation

3. Better one:

RMI is a better approach compared to RPC, especially with larger programs as it provides a cleaner code that is easier to identify if something goes wrong.




---

c.

