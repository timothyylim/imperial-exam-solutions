# Section A
### 1a)

1. extends Thread:

your thread creates unique object and associate with it

2. implements Runnable:

it shares the same object to multiple threads

Another thing to note, since you can extend only one class in Java, if you extends Thread, you can't extend another class. 
If you choose to implement Runnable, you can extend class then.

http://stackoverflow.com/questions/17311842/why-there-are-two-way-of-using-thread-in-java

### bi)

```
CARD = (pay[i:1..4] -> COUNT[i]),
COUNT[i:1..4] = (print_ticket[i]->CARD
				|when i<4 pay[1] -> COUNT[i+1]
				|when i<3 pay[2] -> COUNT[i+2]
				|when i<2 pay[3] -> COUNT[i+3]).
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


