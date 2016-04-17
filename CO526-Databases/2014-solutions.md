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
Since  G -> B
ABGH -> B => AGH -> B
ABGH -> C => AGH -> C
```

```
S'' = {
  AGH   -> B,
  AGH   -> C,
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

Redundant FD X-> A is equivalent to the transative closure of other FDs (i.e. just cancel out transative functions)

```
Since B -> F and B -> D
B -> B => 0

Since F -> B and B -> D
F -> D => 0
```

```
S''' = {
  AGH   -> B,
  AGH   -> C,
  B     -> D,
  B     -> E,
  B     -> F,
  C     -> H,
  E     -> D,
  F     -> B,
  G     -> A,
  G     -> B
  }
```

That's the minimal cover, I guess??


### 4 aii)


