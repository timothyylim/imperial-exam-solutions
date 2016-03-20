# Section A
### 1a)

class MyThread extends Thread { … } Thread a = new MyThread();

Manages a single thread; threads can be created and deleted dynamically.

class MyRun implements Runnable { … } Thread b = new Thread(new MyRun());

Java does not allow multiple inheritance, so sometimes it’s better to implement interface Runnable instead.

### bi)

```
PARKING_METRE = (pay[i:1..4] -> PARKING_METRE[i]),
PARKING_METRE[i:1..4] = (when i < 4 pay[1] -> PARKING_METRE[i+1]
						|when i < 3 pay[2] -> PARKING_METRE[i+2]
						|when i < 2 pay[3] -> PARKING_METRE[i+3]
						|print_ticket[i] -> PARKING_METRE).
```

### bii)

```
MILKSHAKE = (icecream->banana->MADE
			|ice_cream->strawberry-> MADE),

MADE = (mix -> milk -> blend-> SERVABLE
	   |mix -> SERVABLE
	   |bannana-> MADE
	   |strawberry-> MADE),

SERVABLE = (serve -> MILKSHAKE).
```

### biii)

```
property SAFE = (start->STARTED
				|end -> HOLIDAY
				|read -> rest ->STARTED
				|surf -> SURF
				|rest -> STARTED),

HOLIDAY = (start -> STARTED),

STARTED = (end -> HOLIDAY
		  |read -> rest ->STARTED
		  |surf -> SURF),

SURF = (surf -> SURF
		|rest -> STARTED).
```

### 1c
♦  Serially reusable resources:
the processes involved share resources which they use under mutual
exclusion.

♦  Incremental acquisition:
processes hold on to resources already allocated to them while waiting
to acquire additional resources.

♦  No pre-emption:
once acquired by a process, resources cannot be pre-empted (forcibly
withdrawn) but are only released voluntarily.

♦  Wait-for cycle:
a circular chain (or cycle) of processes exists such that each process holds a resource which its successor in the cycle is waiting to acquire.


### 2ai)

```
property SAFE = (lock -> LOCKED[0]),

LOCKED[i:0..1] = (when (i<1) correct_code -> unlock -> SAFE
		| when (i<1) incorrect_code -> LOCKED[i+1]
		| when (i==1) alert -> STOP).
```

### ii)
```
ELECTRICITY_BILL = (enter_account_details -> OPTIONS),
OPTIONS = (enter_meter_reading -> METER
		  |make_payment -> PAYMENT),
METER = (enter_new_reading -> PAYMENT),
PAYMENT = (pay -> finish -> ELECTRICITY_BILL).
```

### iii)
```
const MAX = 3

PATIENT = (request -> ({receive, contact}-> PATIENT)).

PHARMACIST(N=0) = P[N],
P[n:0..3] = (request ->
			(when (n<MAX) refill[n+1] -> send -> P[n+1]
			|when(n>=MAX) assess -> contact -> STOP
			|when (n>=MAX) assess -> send -> PHARMACIST)).

||PRESCRIBE = (PATIENT || PHARMACIST(0))/{send/receive}.
```

### iv)
```
const MAX = 3
PENALTIES = TRIES[0],
TRIES[i:0..MAX] = (when(i<MAX) team1.shoot -> team2.shoot -> TRIES[i+1]).

TEAM(S=0) = SCORE[S],
SCORE[n:0..MAX] = (when (n<MAX) shoot -> score -> SCORE[n+1]
				  |when(n<MAX) shoot -> miss -> SCORE[n]
				  |end -> TEAM).

||SHOOTOUT = (team1:TEAM || team2:TEAM || PENALTIES)@{team1.shoot,team2.shoot}.
```

### 2b)

```
READING = (read -> READING).
WORKING = (program -> WORKING
		|think -> WORKING).

||HOLIDAY = (READING||WORKING).
```

### 2c)

Only the monitor lock of the object on which wait() is called is released, any other monitor locks held by the current thread are unaffected.
