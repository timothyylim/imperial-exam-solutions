### 1

b.i.

```
DOUBLE = (in[i:1..2] -> out[i*2] -> DOUBLE).
```

b.ii.

```
SWITCH = (on -> TURNT
		| off -> SWITCH),

TURNT = (on -> TURNT
		|off -> SWITCH).
```

b.iii.

```
PROCESS = (start -> (end -> STOP | stop -> PROCESS| fail-> ERROR)).
```

b.iv.

```
OVERFLOW = COUNT[0],
COUNT[i:0..5] = (when i<4 inc -> COUNT[i+1]
				|when i == 4 inc -> ERROR).
```

c.i.

```
GAME = (choose[i:1..3] -> (when (i==2) win -> STOP)).
```

c.ii.

```
CYCLE(N=4) = S[0],
S[i:0..3] = (out[i] -> S[(i+1)%N]).
```

c.iii.

```
DOG = (bark -> attack -> DOG).

||DOGS = (fido:DOG||rover:DOG)/{attack/{fido,rover}.attack}.
```

c.iv.

```
PERSON = (sleep -> dream -> PERSON
		 |wake -> work -> PERSON).
INSOMNIA = STOP + {sleep}.

||SEATTLE = (PERSON || INSOMNIA).
```

### 2

b.

```
BUFF = COUNT[0],
COUNT[i:0..8] = (when i<8 put[i] -> COUNT[i+1]
		|when i == 8 get[i] -> COUNT[0]).
```

c.

```
class Buffer {

	public static int N = 8;
	private char[] arr;
	
	public synchronized void put(char ch) throws InterruptedException{
		while (arr.length() == N) wait();
		arr.append(ch);
		notifyAll();
	}
	
	public synchronized char[] get() throws Interrupted Exception{
		while (arr.length < N) wait();
		char[] arr_out = arr;
		Arrays.fill(arr, null);
		return arr_out;
		notifyAll();
	}
	
```

d.

```
BUFF = COUNT[0],
COUNT[i:0..8] = (when i<8 put[i] -> COUNT[i+1]
		|when i == 8 get[i] -> COUNT[0]
		|when i>0 getone[1] -> COUNT[i-1]).
```
