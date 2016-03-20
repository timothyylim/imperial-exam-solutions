# Section A
### 1a)

Alphabet extension is used to extend the implicit alphabet of a process to include actions that are not used by it. It is used to prevent unwanted free actions from occurring when composing it with other processes. Since, after alphabet extension, two processes might share an action that does not occur in one of them, that action will not occur in the composite process either.

### bi)

```
MILK = LEVEL[4],
LEVEL[i:0..4] = (when i > 0 half_glass -> LEVEL[i-1]
        |when i > 1 glass -> LEVEL[i-2]
        |when i == 0 shop -> LEVEL[4]
        |level[i] -> LEVEL[i]).
        
```

### bii)

```
RANCID = COUNT[0],
COUNT[i:0..4] = (when (i<4) nextDay -> COUNT[i+1]
        |when (i<4) {glass, half_glass,shop} -> COUNT[0]
        |when (i==4) shop -> COUNT[0]
        |{glass, half_glass} -> ERROR)
        
        
```

### biii)

```                                                                                                                                                                                                                  
SHOPPING = (shop -> cloudy -> {beer,milk} -> SHOPPING
      |shop -> rainy -> milk-> SHOPPING
      |shop -> sunny -> beer-> SHOPPING).
```

### 2

a.i.

```
property FILE = (open -> OPEN
    |close -> FILE),

OPEN = (read -> OPEN
       |close -> FILE
       |write -> DIRTY),

DIRTY = (read -> DIRTY
  |write -> DIRTY
  |flush -> OPEN).
```

a.ii.

```
const MAX = 4
SEQ_READ(N=2) = (poen -> OPEN[N]),
OPEN[i:1..MAX] = (read -> OPEN[i-1]),
OPEN[0] = (close -> END).

||CONCAT = (a: SEQ_READ(2) || b:SEQ_READ(3))
/{open/a.open,close/b.close,continue/{a.close,b.open}}.
```

a.iii.

```
SPACE_HOG = (new -> outOfMemory -> SPACE_HOG
      |new -> reference -> SPACE_HOG).

SPACED_OUT = STOP + {outOfMemory}.

||TOGETHER = (SPACE_HOG||SPACED_OUT).
```

b.

Simply put, it depends on why your threads are waiting to be notified. Do you want to tell one of the waiting threads that something happened, or do you want to tell all of them at the same time?

In some cases, all waiting threads can take useful action once the wait finishes. An example would be a set of threads waiting for a certain task to finish; once the task has finished, all waiting threads can continue with their business. In such a case you would use notifyAll() to wake up all waiting threads at the same time.

Another case, for example mutually exclusive locking, only one of the waiting threads can do something useful after being notified (in this case acquire the lock). In such a case, you would rather use notify(). Properly implemented, you could use notifyAll() in this situation as well, but you would unnecessarily wake threads that can't do anything anyway.

http://stackoverflow.com/questions/37026/java-notify-vs-notifyall-all-over-again

```
Consider the following piece of code that's executed from multiple parallel threads:

synchronized(this) {
    while(busy) // a loop is necessary here
        wait();
    busy = true;
}
...
synchronized(this) {
    busy = false;
    notifyAll();
}

```

It can be made more efficient by using notify():
```
synchronized(this) {
    if(busy)   // replaced the loop with a condition which is evaluated only once
        wait();
    busy = true;
}
...
synchronized(this) {
    busy = false;
    notify();
}
```

### 3

a.

```
BUFF = COUNT[0],
COUNT[i:0..8] = (when i>0 get -> BUFF[i-1],
    |when i<8 put -> BUFF[i+1],
    |swap[i] -> BUFFER[i]).
```

b.

```
public class MyBuffer implements Buffer {
  private char[] chars;
  private int curr = 0;
  private int used = 0;

  public synchronized void put(char ch) throws InterruptedException {
    while (used == N) wait();
    used++;
    chars[curr] = ch;
    curr = (curr + 1) % N;
    notifyAll();
  }

  public synchronized char swap(char[] ch, int s) {
    while (used + s >= N || s >= used) wait();
    char[] ans;
    for (int i = 0; i < s; i++) ans[i] = get();
    for (int i = 0; i < s; i++) put(ch[i]);
    return ans;
  }

  public synchronized char get() throws InterruptedError {
    while (used == 0) wait();
    used--;
    char ans = chars[curr];
    curr (curr + N - 1) % N;
    return ans;
  }
}
```

c.

### 4

a.

```
public synchronized void aquireWrite() throws InterruptedException{
  while (readers > 0 || writing) wait();
  writer = true;
}

public synchronized void aquireRead() throws InterruptedException{
  while (writer) wait();
  readers++;
}

// how to share lock?
```

b.

```
public synchronized void releaseRead(){
  readers--;
  if(readers ==0) notify();
}

public synchronized void releaseWrite(){
  write = false;
  notifyAll();
}
```

