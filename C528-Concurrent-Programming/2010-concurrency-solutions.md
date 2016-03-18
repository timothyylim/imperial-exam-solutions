### 1

a.

b.i.

```
FLIGHT = (seatBeltSignOff -> OTHER
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

```

c.ii.

```

```

c.iii.

```

```
