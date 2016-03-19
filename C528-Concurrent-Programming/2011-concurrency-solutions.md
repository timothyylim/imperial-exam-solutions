### 1 

a.

Non-deterministic choice can be represented in FSP by the '|' symbol. This means either the action before the symbol could have occured or the action after.

This is important because in some systems it is impossible to predic the order of actions and we need to model both possibilities.

b.i.

```
TALK = (arrive -> front -> TALK
       |begin -> BEGUN),
BEGUN = (arrive -> back -> BEGUN).
```

b.ii.

```
NEVER = (arrive -> ERROR
	|on -> ERROR
	|time -> ERROR).
```

b.iii.

```
LCHAN = (in -> out -> LCHAN
	| disconnect -> STOP 
	| in -> LCHAN).
```

b.iv.

```
CUBE = CUBE[0],
CUBE[i:0..5] = (when i < 4 [i*i*i] -> CUBE[i+1]
			|when i ==4 [i*i*i] -> STOP).
```


c.i.

```
OVERFLOW = CAPACITY[0],
CAPACITY[i:0..3] = (drip -> CAPACITY[i+1]).
```

c.ii.

```
BIKE = (start->(stop->STOP | faster->slower->BIKE)).
```

c.iii.

```
BLOCK = STOP + {north}.
TRAIN = (north -> move -> TRAIN | south -> move -> TRAIN).

|| SYS = (BLOCK || TRAIN).
```

c.iv.

```
EXIT = (in->out -> EXIT).
|| OR = (a:EXIT || b:EXIT) /{in/{a.in, b.in}}.
```


### 2

a.i.

```
TEA_ROBOT = (sugar_please[i:1..3] -> SUGAR[i]),
SUGAR[i:1..3] = (when i > 1 sugar -> SUGAR[i-1]
		|when i ==1 sugar-> TEA_ROBOT).
```

a.ii.

```
property PROPER_TEA = (milk -> tea -> (drink -> PROPER_TEA | sugar -> drink -> PROPER_TEA)) + {slurp}.
```

b.i.

```
SAFE = (sip -> (tooHot -> SAFE | hot -> drink -> SAFE)).
```

b.ii.

```
property SAFE = (sip -> (tooHot -> SAFE | hot -> drink -> SAFE)).
```

The difference is that part ii. is defined as a property and therefore will specifically not allow any action to occur out of the order specified, and will label their terminal states as errors.

c.i.

notify() and notifyAll() 





































































TEA_ROBOT = (sugar_please[i:1..3] -> SUGAR[i]),
SUGAR[i:1..3] = (when i > 1 sugar -> SUGAR[i-1]
				|when i == 1 sugar -> TEA_ROBOT).


### 3

a. 

b.

```
ALLOC = OPEN[0],
OPEN[i:0..MAX] = (when i > 0 get -> OPEN[i-1]
		|when i < MAX put -> OPEN[i+1]
		|close -> CLOSED[i]),
CLOSE[i:0..MAX] = (service -> OPEN[i],
		when i < MAX put -> CLOSE[i+1]).


||COMMONROOM = ({xavi,yael,zak}:MEMBER||wally:TECHNICIAN||saucer:ALLOC||cup:ALLOC).

```

c. 

```
public class Allocator{

	int capacity;
	int used = 0;
	
	public void build(int n){
		capacity = n;	
	}
	
	public synchronized void get()
		throws InterruptException{
		
		while(used>= capacity) wait();
		used++;
		notifyAll()
	}	
	
	public synchronized void put()
		throws InterruptException{
		used--;
		notifyAll()
	}
}


public class Member{
	
	public void get (Allocator a){
		a.get();
	}
	
	public void put (Allocator a){
		a.put();
	}
}


```

c.

```
xavi.cup.get
wally.cup.close
wally.saucer.close

// Xavi is waiting to get the saucer but can't because the saucer is closed. Wally is waiting for all the cups to be returned to service the machine but Xavi won't give up his cup without getting a saucer. A modern tragedy.
```


