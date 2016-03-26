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

# 3



# 4
