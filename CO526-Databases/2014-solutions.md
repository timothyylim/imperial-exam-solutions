### 4 ai)

```
S = {
  ABGH  -> BC,
  B     -> BDEF,
  C     -> H,
  E     -> D,
  F     -> BD,
  G     -> AB
  }
  
```

Compute the minimum cover Sc of S

1 Rewrite S to an equivalent set of FDs which only have a single attribute on the RHS of each FD:

```
S' = {
  ABGH  -> B,
  ABGH  -> C,
  B     -> B,
  B     -> D,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  F     -> D,
  G     -> A,
  G     -> B
  }
```

2 Simplify LHS

```
Since G -> B,
ABGH -> B => 0

B -> B is redundant

Since G -> A and G -> B,

ABGH -> C => GH -> C

We can also remove B -> B

```

```
S'' = {
  GH    -> C,
  B     -> D,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  F     -> D,
  G     -> A,
  G     -> B
 } 
```

3 Find minimal cover by using transitivity

```
Since B -> E and E -> D, we can remove B -> D

Since F -> B and B -> E and E -> D, we can remove F -> D

The minimal cover is therefore:

Sc = {
  GH    -> C,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  G     -> A,
  G     -> B
 } 
 
```

### 4 aii)

```
G has to be in the candidate key because nothing causes G

GH+ = ABEFDCGH
GC gets GH so GC is also a candidate key.
```


### 4 aiii)

Decompose into 3NF

```
Candidate keys: GH, GC

Thus ABDEF are non prime 

and CGH are prime.

The minimal cover:

Sc = {
  GH    -> C,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  G     -> A,
  G     -> B
 } 

Since B is not a superkey and EF is non prime, we can decompose

R1(B,E,F)

Since E is not a superkey and D is non prime, we can decompose

R2(E, D)

Similarly

R3(G, A, B)

Leaving

R4(G,H,C)

```


### 4 aiii)

Decompose into BCNF

```
C -> H violates BCNF because C is not a candidate key

R5(C,H)

Leaving

R6(G,C)

You lose the FD GH->C
```

### 4 bi)

Backward scan for recovery:


| log                      | action         | 
| -------------------------|:-------------:| 
| c3                       | c = {3}       | 
| w3[cB.pop=11,020,00]     |  D = {cB} no change to cB | 
| w2[cR.pop=150,100,000]   |  cR.pop-> 150,100,00 | 
| c1                       | c = {1,3}       | 
| w2[cH.pop=7,120,000]     | cH.pop -> 7,120,000      | 
| w3[cET,...]              |  D = {cB, cET}, no change to cET      | 
| w2[cB,...]               |  no change as cB as cB exists in D      | 
| w4[cCH, pop=7208999]     | cCH.pop -> 7208999 |
| w1[cCH, ...]             | D = {cB, cET, cCH}, no change to cCH as it exists in C already |
| w1[cR,..]                | No change as c1 is already committed |
| w4[cR,..]                | No change to cR as cR is in D |

population figures after recovery:

| code                     | population         | 
| -------------------------|:------------------:| 
| CH                       | 7 208 999         | 
| R                     | 150 100 000         | 
| B                     | 10 170 241        | 
| ...                      |          | 
| ET                       |   63 575 107       | 
