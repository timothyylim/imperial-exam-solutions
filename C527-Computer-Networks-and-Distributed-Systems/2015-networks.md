# 1

a.

What Are The Advantages Of POP?
Being the original protocol, POP follows the simplistic idea that only one client requires access to mail on the server and that mails are best stored locally. This leads to the following advantages:

- Mail stored locally, i.e. always accessible, even without internet connection
- Internet connection needed only for sending and receiving mail
- Saves server storage space
- Option to leave copy of mail on server
- Consolidate multiple email accounts and servers into one inbox
- this is mo!

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

no idea.


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

 In RMI applications, if no security manager is set, stubs and classes can only be loaded from local classpath – protect application from downloaded code

---

lecture slides

b.

At the most basic level, RMI is Java's remote procedure call (RPC) mechanism. RMI has
several advantages over traditional RPC systems because it is part of Java's object oriented
approach. Traditional RPC systems are language-neutral, and therefore are essentially leastcommon-denominator
systems so they cannot provide functionality that is not available on
all possible target platforms.


RMI is focused on Java, with connectivity to existing systems using native methods. This
means RMI can take a natural, direct, and fully powered approach to provide a distributed
computing technology that allows us to add Java functionality throughout the system. To
get the cross-platform portability that Java provides, RPC requires a lot more overheads than
RMI. RPC has to convert the arguments between architecture so that each computer can use
its native datatype. 

RMI’s biggest limitation is it can only call methods in Java. To call
methods written in other languages it has to rely on other technologies like JNI, JDBC,
RMI-IIOP, RMI-IDL etc. Whereas RPC does not translate well into Distributed object
systems, where program-level objects residing in different address space is needed.

http://itgs.tistory.com/attachment/1406296529.pdf
