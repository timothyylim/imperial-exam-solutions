### 1

### a i) 

ICMP - allows routers to send control/error messages to other routers/hosts and provide feedback about communication problems (e.g. no guarantee of delivery, control message return) 

For general knowledge:

- ICMP
  - Internet Control Message Protocol - messages which generally contain information about routing difficulties with IP datagrams or simple exchanges such as time-stamp or echo transactions.

- Dynamic Host Configuration Protocol 
  - provides Internet hosts with configuration parameters. DHCP is an extension of BOOTP. DHCP consists of two components: a protocol for delivering host-specific configuration parameters from a DHCP server to a host and a mechanism for allocation of network addresses to hosts. 

- Address Resolution Protocol / Reverse Address Resolution Protocol 
  - to initialize the use of Internet addressing on an Ethernet or other network that uses its own media access control (MAC). ARP allows a host to communicate with other hosts when only the Internet address of its neighbors is known. Before using IP, the host sends a broadcast ARP request containing the Internet address of the desired destination system. 


ICMP relates to the Network Layer of the OSI Model.

### a ii)

Frame delimiter - indicate start/end of frame (protocol data unit of the data link layer). Comes after the preamble in the ethernet packet. 

Preamble: establish synchronization


### a iii)

Simple Mail Transfer Protocol (SMTP) is a protocal used by Mail Transfer Agents (e.g. Exchange) and Mail User Agents (Outlook, Thunderbird) for delivering mail from one system to another.

two parties communicate using TCP and port 25.

SMTP relates to the application layer.



#### a iv)

Think of a routing table like a map for each little router so it can figure out where in the world he is. 

In computer networking a routing table is a data table stored in a router or a networked computer that lists the routes to particular network destinations, and in some cases, metrics (distances) associated with those routes. The routing table contains information about the topology of the network immediately around it.

Routing tables refer to the network layer.

---

### b i) 

Medium Access Control - Sublayer of the data link layer. I

Network links can be divided into two categories: those using point-to-point connections and those using broadcast channels. In any broadcast network, the key issue is how to determine who gets to use the channel when there is competition for it.

The protocols used to determine who goes next on a multiaccess channel belong to a sublayer of the data link layer called the MAC (Medium Access Control) sublayer. 

### b ii)


