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

Trying without GH -> B: GH+ = GHCBADEF gets the same closure, so we can remove it

Trying without GH -> C: GH+ = GHBDEFAB does not get C, so we can't remove GH -> C  

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

B+ = DEF

Trying without B -> D: B+ = EFD gets the same closure so we can remove it

S''' = {
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
 


Trying without B -> E: B+ = FD does not get the same closure so we cannot remove it

Trying without B -> F: B+ = ED does not get the same closure so we cannot remove it

C+ = H

Can't remove anything

E+ = D

Can't remove anything

F+ = BED

Trying without F -> B: F+ = D does not get the same closure so we cannot remove it

Trying without F -> D: F+ = BED gets the same closure so we can remove it

S'''' = {
  GH    -> C,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  G     -> A,
  G     -> B
 } 
 
 
G+ = ABEDF

Trying without G -> A can't remove as there is no A on the RHS

Trying without G -> B, can't remove as A will never get B

Minimal cover:

S''''' = {
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


