### 1 a)

```
π iso_code, cname, net_assets (company ⨝ office ⨝ public_company)


```

### 4 ai)

```
S = {
      A   -> DEGH,
      AH  -> H,
      B   -> F,
      CF  -> AB,
      E   -> G,
      EH  -> D,
      GH  -> A
}
```

1 Rewrite RHS

```
S = {
      A   -> D,
      A   -> E
      A   -> G,
      A   -> H,
      AH  -> H,
      B   -> F,
      CF  -> A,
      CF  -> B,
      E   -> G,
      EH  -> D,
      GH  -> A
}

```

2 Rewrite LHS

```
Since A -> H, 
AH -> H => A -> H 
and we can remove one of the A -> H

S' = {
      A   -> D,
      A   -> E
      A   -> G,
      A   -> H,
      B   -> F,
      CF  -> A,
      CF  -> B,
      E   -> G,
      EH  -> D,
      GH  -> A
}
```

3 Find minimal cover using transitivity

```
Since A -> E, E -> G,
A -> G => 0

S'' = {
      A   -> D,
      A   -> E,
      A   -> H,
      B   -> F,
      CF  -> A,
      CF  -> B,
      E   -> G,
      EH  -> D,
      GH  -> A
}

```
