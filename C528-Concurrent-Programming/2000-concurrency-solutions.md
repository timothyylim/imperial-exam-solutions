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

