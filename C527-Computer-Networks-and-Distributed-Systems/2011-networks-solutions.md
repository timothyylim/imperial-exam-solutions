### 1 ai)

Broadband networks uses different frequency bands to transmt analogue data by modulating an analogue carrier wave.

Channel can be shared among multiple usrs.

Physical Layer. 


### 1 aii)

A frame that is passed around a ring to allow the host to broadcast dataframes on the medium.

Sender removes frame on return so that it doesn't congest the ring.

Data Link. 

### 1 aiii)

Transparent Spanning Tree Bridges use Backwards Learning to build a table of hosts and links. 

It does this by reading the destination and source addresses of the frames. Over time, all hosts should send frames and therefore it creates a complete table of hosts and links for every bridge.

Backward learning allows bridges to operate transparently tot he network hosts who need not be aware of their existence.

Backwards learning is related to the Data Link Layer. 

### 1 aiv)

ARP - Address Resolution Protocol

ARP is a way to ask for IP/data link address mappings for LAN

```
If host A has no entry for host B,

A will broadcast an ARP address - requesting data link address for B's IP

B recognizes its IP address - returns ARP response with its data link address

B also caches A's data link/ IP address mapping
```

ARP relates to the network layer.


### 1 a v)

A top-level domain (TLD) is one of the domains at the highest level in the hierarchical Domain Name System of the Internet. e.g. .com

Application Layer.


### 1 bi)

Carrier Sense Multiple Access is a protocol to share a medium among multiple nodes.

Each node monitors the medium and only transmits when the medium is idle.

One can contrast CSMA with ALOHA, where nodes send data immediately when it is avaliable. 

Collision Detection means to listens to the medium whilst sending to see if somebody else is transmitting at the same time.

### 1 biii)


### 2 ai)


Classless-Inter-Domain routing is method for allocating IP addresses and IP packets.

It works by splitting the world into 4 zones (Europe, N. America, Central/South America and Future Use (Sorry, Africa)). 

Size according according to need, not just fixed classes (hence, the name Classless). 

Its goal was to slow the growth of routing tables on routers across the Internet, and to help slow the rapid exhaustion of IPv4 addresses.


### 2 aii)

C

### 2 aiii)

255        .   255         .  224         .  0
1111 1111      1111 1111      1110 0000      0000 0000

subnet space will be from the 13 binary values, so do 2^13 - 2


Or..

255-224+1 = 32 = 2^5

2^8 x 2^5 = 2^13

2^13 - 2 = 8190

### 2 aiii)

255.255.248.0

### 2 aiv)

2^11 - 2 = 2046

### 2 b)

