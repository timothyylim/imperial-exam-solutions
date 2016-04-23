# Pt. 4 Network Layer

- Transparent vs Source Routing Bridges
- Hub vs Switches vs Routers
- Adaptive vs Non-Adaptive Routing
  - Distance Vector Calculations
- ARP vs DHCP vs ICMP


---


Client:

```
Do everything inside main:

possibly need to do something with value passed to main e.g.
int Variable = Integer.parseInt(args[0]);


Always:
interfaceName Object = Naming.lookup(ServerURL);

Possibly need a loop (while (true)) that performs the main action e.g. 
collect info using functions provided and then send them onto the remote object: 
e.g.
Object.report(variable1,variable2,variable3) //where report is a provided function
and passes info to the remote host
```

Server:

```
Naming.rebind(ServerURL,object);
```

Both:

```
if System.getSecurityManager == null
  System.setSecurityManager(new RMISecurityManager())
  
try{}catch{}

public static void main(){}
```
