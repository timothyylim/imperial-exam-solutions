### 3 bi)

To figure out if it is serializable, look for either of the following:

1. Read followed by a Write
2. Write followed by another Write

Only conflict found:

w1(aG-CWQS), r3(aG-CWQS) 

waits for graph:

```
T1 --> T3
```

No cycle, nice!

We can see that it is serializable (CSR).

And for recoverability, consider if the commits depend on anything:

The commit c3 depends r1[aG-CWQS] and w1[aG-CWQS], (which are not yet committed) and is therefore not recoverable due to dirty read and dirty write.


### 3 b ii)

The only conflict found between T1 and T2:

w1[aG-FDWC], r2[aG-FDWC]

A deadlock can only occur when process A is holding a lock that is held by process B whose release is dependent on process A's actions.

Since there is no cycle, there can never be a deadlock between T1 and T2.

### 3 b iii)

Find the conflict pairs:

```
w1(aG-FDWC) <--> r2(aG-FDWC)
r2(aG-FXDC) <--> w3(aG-FXDC)
w3(aG-CWQS) <--> r1(aG-CWQS)
```

Consider the following history:

```
r1(aG-CWQS),
w1(aG-CWQS),
r1(aG-FDWC),
r2(aG-FDWC),
r3(aG-FXDC),
w3(aG-FXDC)
```

T1 holds ```wl1 [aG-CWQS]```
T2 holds ```rl2 [aG-FDWC]```
T3 holds ```wl3 [aG-FXDC]```

Waits for graph:

```
      T3   <------ rl2[aG-FXDC] -------------- T2 
      |                                         ^
      |                                         |
      |---rl3[aG-CWQS] --> T1 ---- wl1[aG-FDWC]--
```
