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




# 3

# 4
