### 1ai)
```
ALARM = COUNT[5],
COUNT[i:0..5] = (when (i>1) tick[i] -> COUNT[i-1]
				|when (i==1) tick[i] -> beep -> STOP
				|off -> STOP
				|snooze -> ALARM).
```

### ii)

```
PROGRAM = (write -> COMPILE),

COMPILE = (compile -> COMPILED
			|compile->ERR),
COMPILED = (ok -> run-> STOP),

ERR = (error[1] -> fix[1] -> (compile->STOP|error[2]->fix[2]->compile->COMPILED)).

or 

PROGRAM = (write->COMPILE[1]),
COMPILE[i:1..3] = (compile -> OK
		|when(i<3) compile -> error[i] -> fix[i] -> COMPILE[i+1]
		|when(i==3) compile -> ERROR),
OK = (ok->run->STOP).
```

### iii)

```
property HAPPY = (wakeup -> eat ->EATEN),
EATEN = (sleep -> HAPPY
		|rest-> EATEN
		|surf->SURF
		|read -> READ),
READ = (read->READ
		|eat->EATEN),
SURF = (surf ->SURF
		|eat -> EATEN).
```

### bi)

```
TURTLE = (north -> move -> TURTLE
		| south -> move -> TURTLE).

CONSTRAIN = STOP + {north}.

||SYS = (CONSTRAIN || TURTLE).
```

### ii)

```
GATE = (in->out->GATE).

||AND = (a:GATE || b:GATE)/{out/{a.out,b.out}}
```

### iii)

```
set A = {heads,tails}

HeadsOrTails = PICK,
PICK = (pick[i:A] -> FLIP[i]),
FLIP[i:A] = (flip[j:A] -> RESULT[i][j]),
RESULT[i:A][j:A] = (when (i==j) win -> HeadsOrTails
					|when (j!=i) lose -> HeadsOrTails).
```

### ci)

synchronised prevents multiple invocations of synchronised methods on the same object from interleaving: threads calling synchronised methods must acquire the object’s monitor lock.
					
wait() suspends the current thread and releases the monitor lock. A thread calling wait on an object must own its monitor lock. Execution is resumed after a call to notify() or notifyAll().
When synchronising conditions, the usual pattern is:

```					
synchronised void doStuff() {
    while (!cond) {


					
wait(); }
					
}

```
					
Whenever the condition changes, notify() is called to wake up the current thread. wait() must be placed in a loop since the thread that woke up is not guaranteed to reacquire the monitor lock instantly, thus another condition can change the condition in the meantime.



### ii)

Yes - when the first thread calls wait, it releases the monitor lock, so the second thread is able to acquire it, enter the function, print the message and get blocked on wait().

### 2a)

```
const M = 10
range B = 0..M
LIBRARY_ACC = ACC[0][0],
ACC[i:B][f:0..1] = (when(f==0 && i<M) borrow -> ACC[i+1][f]
            |when(i>0) return -> ACC[i-1][f]
            |when(f==0) freeze -> ACC[i][1]
            |when(f==1) unfreeze -> ACC[i][0]).
```

OR

```
const M = 10
range B = 0..M

LIBRARY = LIBRARY[0],
LIBRARY[i:B] = (when i < M borrow -> LIBRARY[i+1]
			   |when i > 0 return -> LIBRARY[i-1]
			   |freeze -> FROZEN[i]),
FROZEN[i:B] = (freeze -> FROZEN[i]
			  |unfreeze-> LIBRARY[i]
			  |when i > 0 return -> FROZEN[i-1]).
```

### 2b)

```
class Library{

	int final MAX = 10;
	int current = 0;
	boolean frozen = false;
	
	public synchronized void borrow()
		throws InterruptedException{
			while (current == MAX || frozen) wait();
			current++;
			notifyAll();
		}

	public synchronized void return()
		throws InterruptedException{
			while (current == 0) wait();
			current--;
			notifyAll();
		}
		
	public synchronized void freeze(){
		freeze = true;
		notifyAll();
	}
		
	public synchronized void unfreeze()
		freeze = false;
		notifyAll()
	}
}
```

### 2ci)

```
||SYSTEM = (ADMIN || lina:MEMBER ||will:MEMBER || {lina,will}::LIBRARY_ACC)
/{freeze/{lina.freeze,will.freeze},unfreeze/{lina.unfreeze,will.unfreeze}}.
```
### 2cii)
```
property NO_BORROW_WHEN_FROZEN = ({borrow,return}->NO_BORROW_WHEN_FROZEN | freeze->RETURN),
RETURN = (return -> RETURN | unfreeze -> NO_BORROW_WHEN_FROZEN).
```
### 2cii)
```
progress ALWAYS_BORROW = {will.borrow,lina.borrow}
```
### 3a

“A safety property asserts that nothing bad happens during execution. A liveness property asserts that something good eventually happens. Another way of putting this is that safety is concerned with a program not reaching a bad state and that liveness is concerned with a program eventually reaching a good state.”

### b

```
const M=5
const Max = 7

set Arsenal ={arsenal[1..Max]}
set Chelsea = {chelsea[1..Max]}

SUPPORTER = (enter -> dine -> exit -> SUPPORTER).

DININGROOM = DININGROOM[0][0],

DININGROOM[a:0..Max][c:0..Max] = ( when(c==0 && a < Max) arsenal[1..Max].enter -> DININGROOM[a+1][c]
				| arsenal[1..Max].exit -> DININGROOM[a-1][c]
				| when(a==0 && c< Max) chelsea[1..Max].enter -> DININGROOM[a][c+1]
				| chelsea[1..Max].exit -> DININGROOM[a][c-1]).

||PUB = (Chelsea:SUPPORTER||Arsenal:SUPPORTER||DININGROOM).
```

### ci


this needs to be improved:

```
property NOCONFLICT = (arsenal[1..Max].enter -> CONTROL1[1] 
		      |chelsea[1..Max].enter -> CONTROL2[1]),

CONTROL1[i:0..Max] = (  arsenal[1..Max].enter -> CONTROL1[i+1]
			|when(i>1) arsenal[1..Max].exit -> CONTROL1[i-1]
			|when(i==1) arsenal[1..Max].exit  -> NOCONFLICT), 

CONTROL2[i:0..Max] = (  chelsea[1..Max].enter -> CONTROL2[i+1]
			|when(i>1) chelsea[1..Max].exit -> CONTROL2[i-1]
			|when(i==1) chelsea[1..Max].exit  -> NOCONFLICT).
```

### cii

```
property OVERFLOW = CONTROL[0],
CONTROL[i:0..Max] = (when(i>0){Arsenal.enter,Chelsea.enter} -> CONTROL[i+1]
                    |when(i<Max){Arsenal.exit,Chelsea.exit} -> CONTROL[i-1]).
```

### ciii

```
progress TURNOVER1 = {arsenal[1..Max].enter}
progress TURNOVER2 = {chelsea[1..Max].enter}
```

### d 

“When the consumer calls get, it acquires the Buffer monitor lock and then acquires the monitor lock for the full semaphore by calling full.down() to check if there is something in the buffer. Since initially the buffer is empty, the call to full.down() blocks the consumer thread (using wait()) and releases the monitor lock for the full semaphore. However, it does not release the monitor lock for Buffer. Consequently, the producer cannot enter the monitor to put a character into the buffer and so no progress can be made by either producer or consumer – hence the deadlock. The situation described above is known as the nested monitor problem.”

### 4a


### bi

```
const MAX = 4
BUFFER = BUFFER[0],
BUFFER[i:0..MAX] = (when i < MAX put -> BUFFER[i+1]
				   |when i > 0 get -> BUFFER[i-1]
				   |put_all[p:0..MAX-i] -> BUFFER[i+p])
                   |get_all -> BUFFER).

```

### bii

```
const MAX = 4
BUFFER = BUFFER[0],
BUFFER[i:0..MAX] = (when i < MAX put -> BUFFER[i+1]
				   |when i > 0 get -> BUFFER[i-1]
				   |put_all[p:0..MAX-i] -> BUFFER[i+p])
                   |get_all -> BUFFER).

``` 

### biii

```
Class safeBuffer extend Buffer {
Int space = 0;
Int Max = 8;

Int[] buffer = new int[Max];

Public synchronised void put(char ch) throw InterruptedException{
	while(space==Max) wait();
	Buffer[space] = ch;
	space++;
	NotifyAll();
}
Public synchronised void get() throw InterruptedException{
	while(space==0) wait();
	char ch = buffer[space-1];
	buffer[space-1] = null;
	space--;
	notifyAll();
	return ch;
}
Public synchronised void putall ( char[] ch ) throws InterruptedException{
	Int j = ch.length();
	While (space+j>Max) wait();
	for(int i =0;i<j;i++){
		Buffer[space+i] = ch[i];
}
space= j+space;
notifyAll();
}

Public synchronised void getAll() throw InterruptedException{
Int [] temp =  new int[space]
if(space==0 ){
Return temp
}else{

for(int i = 0; i=<space:i++){
			temp[i]=space[i]
			Space[i] = null;
}
Space =0;
Return temp;
}
}
}
```

