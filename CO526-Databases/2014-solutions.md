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

