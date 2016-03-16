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


