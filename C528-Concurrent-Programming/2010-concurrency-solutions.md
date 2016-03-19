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
COUNT[i:TIME] = (when i < MAX-1 t[i] -> COUNT[i+1] 
                |when i == MAX-1 t[i] -> COUNT[0]).
```

c.i.

```
const MAX = 59
range TIME = 0..MAX-1
TIMER = COUNT[0],
COUNT[i:TIME] = (when i < MAX-1 t[i] -> COUNT[i+1] 
                |when i == MAX-1 t[i] -> COUNT[0]).

PROCESS(I=2) = (at[I] -> run -> STOP) + {at[TIME]}.

||SYS = ({a,b}::TIMER || a:PROCESS(2) || b:PROCESS(7))
        /{tick/{a,b}.tick}
        <<{{a,b}.at[t:TIME]}
```

```
	a.t.0
	a.t.1
	a.t.2
	a.t.3
	a.t.4
	a.t.5
	a.t.6
	a.t.7
	a.t.8
	a.t.9
	a.t.10
```

c.ii.

```
To include the range??
```

c.iii.


d. 

```
class Timer{

	final int Max = 60
	int current = 0;
	
	public void synchronized tick()
		throws InterruptException{
			while (current == Max) wait();
			current ++;
		}
		
	public void synchronized reset()
		throws InterruptException{
		
		while (current < Max) wait();
		current = 0;
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
|| BATCH = ({a,b,c}::JOB(3)||{d,e}::JOB(1)||{a,b,c,d,e,}::ALLOC)
```

b.ii.

```
progress JOB(1) = {JOB(1).get}
progress JOB(3) = {JOB(3).get} 
```

b.iii.

```

```

b.iv.

```

```

c.

```
// Still need to add Job

class Allocator{

	private int available;
	
	public void build(int NB){
		available = NB;
	}
	
	synchronized public void get(int n)
		throws InterruptedException{
		
		while (n > avaliable) wait();
		avaliable -= n;
	}
	
	synchronized public void put(int n)
		throws InterruptedException{
		available += n;
		notifyAll();
	}
}
```

### 4 

a.

Liveness and Progress properties are concerned with the program eventually reaching a good state.

A progress property is a subset of the Liveness properties and it asserts that whatever state a system is in, it is always the case that a specified action will eventually be executed.

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

