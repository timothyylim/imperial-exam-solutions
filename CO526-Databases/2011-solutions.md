### 3 bi)

To figure out if it is serializable, look for either of the following:

1. Read followed by a Write
2. Write followed by another Write

Only conflict found:

w1(aG-CWQS), r3(aG-CWQS) 

Serialization graph:

```
T1 --> T3
```

No cycle, nice!

We can see that it is serializable (CSR).

And for recoverability, consider if the commits depend on anything:

The commit c3 depends r1[aG-CWQS] and w1[aG-CWQS], (which are not yet committed) and is therefore not recoverable due to dirty read and dirty write.

