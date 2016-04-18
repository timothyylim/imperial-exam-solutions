### 4 ai)

```
S = {
      AB  -> ACDE,
      ABD -> CEF,
      GH  -> FE,
      E   -> F,
      D   -> B,
      C   -> ABCD
}
```

1 Rewrite RHS to only have one attribute


```
S' = {
      AB  -> A,
      AB  -> C,
      AB  -> D,
      AB  -> E,
      ABD -> C,
      ABD -> E,
      ABD -> F,
      GH  -> F,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> B,
      C   -> C,
      C   -> D
}
```

2 Simplify LHS

```
Since D -> B, 
ABD -> C => AD -> C
ABD -> E => AD -> E
ABD -> F => AD -> F

S'' = {
      AB  -> A,
      AB  -> C,
      AB  -> D,
      AB  -> E,
      AD -> C,
      AD -> E,
      AD -> F,
      GH  -> F,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> B,
      C   -> C,
      C   -> D
}
```

3 Find minimal cover using transitivity

```
S''' = {
      AB  -> A,
      AB  -> C,
      AB  -> D,
      AB  -> E,
      AD -> C,
      AD -> E,
      AD -> F,
      GH  -> F,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> B,
      C   -> C,
      C   -> D
}


Since AB -> C, C -> A
AB -> A => 0

S'''' = {
      AB  -> C,
      AB  -> D,
      AB  -> E,
      AD -> C,
      AD -> E,
      AD -> F,
      GH  -> F,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> B,
      C   -> C,
      C   -> D
}

Since AB -> C, C -> D
AB -> D => 0

S'''' = {
      AB  -> C,
      AB  -> E,
      AD -> C,
      AD -> E,
      AD -> F,
      GH  -> F,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> B,
      C   -> C,
      C   -> D
}

Since AD -> E, E -> F
AD -> F => 0

Since GH-> E, E -> F
GH -> F => 0

Can also remove C -> C

Minimal Cover 

Sc = {
      AB  -> C,
      AB  -> E,
      AD -> C,
      AD -> E,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> B,
      C   -> D
}
```

### 4 aii)

Identify and justify all candidate keys of R

```

```
