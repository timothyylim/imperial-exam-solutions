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
```

### iii)


