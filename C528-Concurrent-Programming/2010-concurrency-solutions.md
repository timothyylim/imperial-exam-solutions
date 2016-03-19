### 1

a.

```
P = (eat-> poop -> vomit -> P).
Q = (drink-> poop ->  vomit -> Q).

|| CONCURRENT = (m:P||n:Q).
```

To guarantee n times m states, you would need to have specific identifiers for the process. For example the answer above without the identifiers would only return four states.


b.i.

```
property FLIGHT = (seatBeltSignOff -> OTHER
		  |sit -> FLIGHT),
OTHER = ({sit,walk}-> OTHER
		|seatbeltSignOn -> FLIGHT).
```

b.ii.

```
BOARDING = (onlineCheckIn -> CHECKED
		   |deskOpen -> OPENED),
OPENED = (onlineCheckIn -> OPENED
		 |checkIn -> OPENED
         |flightClosed -> CHECKED),
CHECKED = (board -> CHECKED
          |takeOff -> STOP).
```

b.iii.

```
const MAX = 3
MILES = MILES[0],
MILES[i:0 .. MAX] = 
    ( when (i< MAX) fly[j:1..MAX-i] -> MILES[j+i]
    | when (i>1) redeem[j:1..i] -> MILES[i-j]
    | mileage[i] -> MILES[i]).
```

b.iv.

```
CABIN = (buyEconomy -> (requestUpgrade -> flyEconomy-> CABIN 
                       |requestUpgrade -> flyBusiness -> CABIN)).
```

c.i.

```
PROGRAM = (write -> WRITTEN),
WRITTEN = (compile -> compile_time_error -> PROGRAM
           |compile -> ok -> COMPILED),
COMPILED = (run -> run_time_error -> PROGRAM  
           |run -> STOP).
```

c.ii.

```
property PROTOCOL = CLOSED,
CLOSED = (open -> OPEN),
OPEN = ({read, write} -> OPEN | close -> CLOSED).
```

c.iii.

```
const MAX = 3
ENTER_PIN = ENTER_PIN[0],
ENTER_PIN[n:0..MAX-1] = 
(pin -> (ok -> ENTER_PIN 
        |nok -> ENTER_PIN[n+1])),
ENTER_PIN[MAX] = (confiscate_card -> STOP).
```

c.iv.

```
const MAX = 1
VAR = VAR[0],
VAR[i:0..MAX] = (read[i] -> VAR[i]
                |write[j:0..MAX] -> VAR[j]).

PROCESS(N=1) = (write[N]->read[i:0..MAX] -> STOP) + {write[i:0..MAX]}.

||INTERFERE = (a:PROCESS(0)
             ||b:PROCESS(1)
             ||{a,b}::VAR)/{read/{a.read,b.read}}.
```

### 2

a.

The alphabet of a process is the set of actions in which it can engage.

b.

```
const MAX = 59
range TIME = 0..MAX-1
TIMER = COUNT[0],
COUNT[i:TIME] = (when i < MAX-1 tick[i] -> COUNT[i+1] 
                |when i == MAX-1 tick[i] -> COUNT[0]
				|at[i] -> COUNT[i]).

PROCESS(I=2) = (at[I] -> run -> STOP) + {at[TIME]}.

||SYS = ({a,b}::TIMER || a:PROCESS(2) || b:PROCESS(7))
        /{tick/{a,b}.tick}
        <<{{a,b}.at[t:TIME]}.
```

c.i.

```

```

```
 tick.0
 tick.1
 a.at.2
 tick.2
 tick.3
 tick.4
 tick.5
 tick.6
 b.at.7
 tick.7
 tick.8
 tick.9
 tick.10

```

c.ii.

The alphabet extension is required in the definition of process to synchronize the actions of PROCESS and TIMER and to prevent the independent execution of 'at' by TIMER.

c.iii.

It will only be able to do {a,b}at[0] since {a,b} is always higher priority and always be avaliable. 

```
 a.at.0
 a.at.0
 b.at.0
 b.at.0
```

d. 

```
class Timer{

	private final int Max = 59;
	private int seconds = 0;
	
	public synchronized void tick(){
		seconds = seconds +1 % Max;
		notifyAll();
	}
	
	public synchronized void at(int t)
		throws InterruptedException {
		
		while (seconds != t) wait();
		
		//Do some shit
	}
}
```

### 3

a. 

class MyThread extends Thread { … }
Thread a = new MyThread();

Manages a single thread; threads can be created and deleted dynamically.

Class MyRun implements Runnable { … }
Thread b = new Thread(new MyRun());

Java does not allow multiple inheritance, so sometimes it’s better to implement interface Runnable instead.

b.i.
```
const NB = 4 // Max number of allocatable blocks
set ALL = {{get,put}[1..NB]}

JOB(B=1) = (get[B]->run->put[B]->JOB)+ALL.

ALLOC = ALLOC[NB],
ALLOC[i:0..NB] = (when (i>0) get[j:1..i] -> ALLOC[i-j] 
				|put[j:1..NB] -> ALLOC[i+j]).

```

```
||BATCH = (small[1..2]:JOB(1)||big[1..3]:JOB(3)||{small[1..2],big[1..3]}::ALLOC).
```

b.ii.

```
progress SMALL = {small[1..3].get[1]}
progress BIG = {big[1..2].get[3]} 

```
b.iii.

```
||BATCH = (small[1..3]:JOB(1)||big[1..2]:JOB(3)||{small[1..3],big[1..2]}::ALLOC)<<(small[1..3].get[1],big[1..2].get[3]).
```

b.iv.

Property 'BIG' may be violated because only small[1..3].get[1] will be called due to it having a higher priority as specified in iii.

c.

```
class Allocator{

	private int available;
	
	public Allocator(int a){
		available = a;
	}
	
	synchronized public void get(int n)
		throws InterruptedException{
		while (n > avaliable) wait();
		avaliable -= n;
	}
	
	synchronized public void put(int n)
		available += n;
		notifyAll();
	}
}

class Job implments Runnable {
	
	Allocator alloc;
	int size;
	
	public Job(int jobsize, Allocator a){
		alloc = a;
		size = jobsize;
	}
	
	public void run(){
		try{
			alloc.get(size);
			// Do some shit
			alloc.put(size);
		}
		
		catch(InterruptedException e){}
	}
}

void build(int NB){
	Thread S1 = new Thread(new Job(1));
	Thread S2 = new Thread(new Job(1));
	Thread S3 = new Thread(new Job(1));
	Thread S4 = new Thread(new Job(3));
	Thread S5 = new Thread(new Job(3));
	
	Allocator alloc = new Allocator(NB);
}
```

### 4 

a.

Liveness and Progress properties are concerned with the program eventually reaching a good state.

A progress property is a subset of the Liveness properties and it asserts that whatever state a system is in, it is always the case that a specified action will eventually be executed.

ex.

Every terminal set contains every action in the alphabet of the process.

b.
```

property FIRST = FIRST[0],
FIRST[i:0 .. 4] = 
    ( when (i< 4) login[j:1..4-i] -> FIRST[j+i]
    | when (i>1) logout[j:1..i] -> FIRST[i-j]).
    
property SECOND = (disable[u] -> login[u]).
```

c.i.

“Once a thread has acquired the lock on an object by executing a synchronized method, that method may itself call another synchronized method from the same object (directly or indirectly) without having to wait to acquire the lock again. The lock counts how many times it has been acquired by the same thread and does not allow another thread to access the object until there has been an equivalent number of releases.”

Excerpt From: byJeff MageeandJeff Kramer. “Concurrency&#8212;State Models &amp; Java Programs, 2nd Edition.” iBooks. 

c.ii.

```
const N = 3
range P = 1..2
range C = 0..N

set VarAlpha = {value.{acquire[P],release[P]}

VAR = VAR[0],
VAR[p:P] = (acquire[p:P]->VAR[p] | release[p:P]->VAR[p]).

LOCK = (acquire->release->LOCK).

||LOCKVAR = (LOCK || VAR).

```

