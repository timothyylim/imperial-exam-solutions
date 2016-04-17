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

Find the superkey

```
GH+ = GHBCDEFA

Trying without GH -> B: GH+ = GHCBADEF gets the same closure, so we can't remove it

Trying without GH -> C: GH+ = GHBDEFAB does not get C, so we can remove GH -> C  

S''' = {
  GH    -> B,
  B     -> D,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  F     -> D,
  G     -> A,
  G     -> B
 } 

B+ = DEF

Trying without B -> D: B+ = EFD gets the same closure, so we can't remove it

Trying without B -> E: B+ = DF does not get E, so we can remove B -> E 

S'''' = {
  GH    -> B,
  B     -> D,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  F     -> D,
  G     -> A,
  G     -> B
 } 



```

3 

### 4 aii)


