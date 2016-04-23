### 1 ai)

SYN is a control bit in a TCP header.

Transport Layer.

### 1 a ii)

When a signal decreases in strength over distance.

note: Repeater solves this

Physical Layer.

### 1 a iii)

A way of encoding a signal by using a clock for synchronization between receiver and sender.

Every binary value is represented by presence or absence of transitions. 

Physical Layer.

### 1 a iv)

Routing strategy that uses dynamic routing.

Each router creates a table with all of its neighbours in the network and updates their distances dynamically.

Network Layer.

### 1 a v)

SFD is part of Ethernet frames IEE802.3 . Header then a delimeter. It allows the receiver to synchronize with the frame even if it misses the start of the preamble. It is usuall 101011.

Data Link Layer.

### 1 a vi)

You use it when you are 'pinging'.

When you 'ping' you send an echo response packet to verify a path works and end host is present.

It allows routers to send control error messages to other routers' hosts.

Network Layer.

### 1 b i)

In data communications, flow control is the process of managing the rate of data transmission between two nodes to prevent a fast sender from overwhelming a slow receiver.

### 1 b ii)

TCP implements flow control with a sliding window size.

This works by using sequence, acknowledgement and window fields of the TCP header. Recipient shoudl not send more than (window sizw - bytes sent).


### 1 b iii)

### 1 b iv)

### 2 a i)

Sharing a medium.

### 2 a ii)

TDM - Time Division Multiplexing. Divide the channel into fixed time slots and encode signals to be sent at different times.

FDM - Frequency Division Multiplexing. Think of radio AM/FM frequencies.

CDMA - Code Division Multiplexing. Everyone talking but in different languages. 

### 2  a iii)

In the transport layer, many packets exist destined for different ports. 

### 2 b i)

An IP address serves two principal functions: host or network interface identification and location addressing.

Media access control address (MAC address), also called physical address, is a unique identifier assigned to network interfaces for communications on the physical network segment. 

### 2 b ii)

1. Class from the IP (B) 
2. Host occupies 16 bits
3. Network occupies 14 bits

### 2 b iii)

ARP.

### 2 b iv)

Default Router: 225 should be 247 because it has to be the same address 1.

DNS Server 1: 192 is a private address and can't be made public.

Can't have non consecutive 1's in a netmask.


### 4 ai)

A remote object registry is a bootstrap naming service that is used by RMI servers on the same host to bind remote objects to names. Clients on local and remote hosts can then look up remote objects and make remote method invocations.

### 4 aii)

 The job of a security manager is to prevent any nasty surprises from remotely loaded classes. Therefore, you only need to install a security manager for RMI if the peer is using the codebase facility to supply classes to you dynamically.

The checks a security manager does (just imagine him as some fat security guard) is the access to
- communications
- files
- control of the virtual machine

 In RMI applications, if no security manager is set, stubs and classes can only be loaded from local classpath, so yes, you can survive without a security manager. Living without the security manager is either unecessarily risky or completely fine depending where you are loading your stubs from. 

### 4 aiii)

In a distributed system, just as in the local system, it is desirable to automatically delete those remote objects that are no longer referenced by any client. This frees the programmer from needing to keep track of the remote objects' clients so that it can terminate appropriately.

### 4 b)

```
public class bedMonitor{

 public static void main(String [] args){
  int Bed = Interger.parseInt(args[0]);
  
  if(System.getSecurityManager() == null){
   System.SetSecurityManager(new SecurityManager());
  }
  
  try{
   iNurse NS = (iNurse)Naming.lookup("rmi//remotehost//NurseStation")
   
   while(true){
    int temp = deviceRead("temp");
    int pulse = deviceRead("pulse");
    
    NS.report(bed,temp,pulse);
    thread.sleep(6000);
    
   }catch(Remote Exception e){System.out.println(e);}
 }

}
```

### 4 aii)

```
public class nurseStation implements iNurse{

 public nurseStation() throws RemoteException{}
 
 public static void main(String [] args){
  
  if System.getSecurityManager() == null {
   System.setSecurityManager(new RMISecurityManager());
  }
  
  try{
   nurseStation NS = new NurseStation();
   Naming.rebind(Serverurl, NS);
  }catch(Exception e){ System.out.println(e);}
  
 }
 
 


}
```




