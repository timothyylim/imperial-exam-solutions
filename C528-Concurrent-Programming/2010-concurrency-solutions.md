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

