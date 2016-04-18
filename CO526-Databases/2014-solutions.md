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
Since G -> A and G -> B,

ABGH -> B => GH -> B
ABGH -> C => GH -> C

We can also remove B -> B

```

```
S'' = {
  GH    -> B,
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

The minimal cover is therefore:

Sc = {
  GH    -> B,
  GH    -> C,
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

### 4 aii)

```
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
  GH    -> B,
  GH    -> C,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  F     -> D,
  G     -> A,
  G     -> B
 } 

Since B is not a superkey and EF is non prime, we can decompose

R1(B,E,F)

Since E is not a superkey and D is non prime, we can decompose

R2(E, D)

Similarly

R3(F, B, D)


```
