### 1 a)
```
πcity,name (located⨝located.country=country.code country)
```

### 1 b)
```
πabbreviation,city,country,established σorganization='NATO'∧type='member' (is_member⨝organization)
```
### 1 ci)

The query gets the countries that have more then 10M inhabitants and not located in Europe with less then 10M inhabitants.

Therefore, the - in the brackets is useless.

|code|
|----|
|CZ|
|R|
|B|
|TR|
|GB|
|ET|

### 1 cii)
```
SELECT code
FROM country
WHERE population > 10,000,000
EXCEPT
(
  SELECT country AS code
  FROM encompasses
  WHERE continent = 'Europe'
  EXCEPT
  SELECT code
  FROM country
  WHERE population > 10,000,000
)
```

### 1 ciii)
```
query(code):-
  more_than_10(code),
  ¬(encompasses(code,Europe,_),
  ¬more_than_10(code)).

more_than_10(code):-
  country(_,code,_,_,pop),
  pop > 10000000.
```

### 1 di)
```
πorganization,country σtype='member' is_member ÷ πcountry σtype='member' ∧ organization='CERN' is_member
```

### 1 dii)
```
SELECT DISTINCT organization
FROM is_member AS x
WHERE type='member' 
AND NOT EXISTS
(
  SELECT *
  FROM is_member AS y
  WHERE type='member'
  AND organization='CERN'
  AND NOT EXISTS 
  (
    SELECT *
    FROM is_member AS z
    WHERE type='member' 
    AND x.organization = z.organization 
    AND x.country = y.country
  )
)
```

### 1 e)

needs to be improved:
update: no, this is correct. the union operator is set based in relational algebra (tested on relax to make sure)

```
π country.capital, country.code (country) ∪ π organization.city, organization.country (organization)
```

### 3 bi)

```
Confclits:          Anomalies:
w1[TR] -> r2[TR]    dirty read
r2[GB] -> w1[GB]    ?

CSR Graph: T1 -> T2 -> T1 therefore not CSR => non-serialisable
```

The results would not be the same if we did Ha vs H1, H2 nor H2, H1. This is evident in the CSR graph hence Ha is non-serialisable. (Inconsistent analysis?) It is also not recoverable because there is a dirty read in T2 which is committed before T1 is committed.

### 3 bii)

```
Confclits:          Anomalies:
r2[CZ] -> w3[CZ]    ?
r2[TR] -> w3[TR]    ?

CSR Graph: T2 -> T3 therefore CSR => serialisable
```

The results would be the same whether we did Hb or H2, H3 so it is serializable. It is also recoverable (ST) because there are no dirty reads or dirty writes.

### 3 biii)

```
Confclits:          Anomalies:
r1[TR] -> w3[TR]    redundant?
r3[TR] -> w1[TR]    redundant?
w3[TR] -> w1[TR]    lost update / dirty write?
r3[GB] -> w1[GB]    ?

CSR Graph: T1 <==> T3 therefore not CSR => non-serialisable
```

The results of Hb would not be the same if we did H1, H3 or H3, H1 instead so Hb is non-serialisable specifically because of the lost update anomaly (w3[TR] is lost). I don't know about the recoverablility.

### 3 biv)

```
r1[TR], w1[TR], r1[GB], r2[CH], r2[GB], r2[CZ], r3[GB], r3[CH], r3[CZ], deadlock

WFG:
w1[GB] is waiting on r2[GB]
r2[TR] is waiting on w1[TR]
w3[CZ] is waiting on r2[CZ]

T1 <==> T2 <-- T3

```

I think other possible solutions exist but this one should work.

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
| w1[cR,..]                | D = {cB, cET, cCH, cR}. No change to cR as cR is in D |
| w4[cR,..]                | No change to cR as cR is in D |

population figures after recovery:

| code                     | population         | 
| -------------------------|:------------------:| 
| CH                       | 7 208 999         | 
| R                     | 150 100 000         | 
| B                     | 10 170 241        | 
| ...                      |          | 
| ET                       |   63 575 107       | 


### 4 bii)

Must have written:

w1[cR], w1[cH] since for UNDO only logs, one must flush all commited data to disk

Might have written:

w4[cCH], w2[cB], w3[cET], w2[cCH], w4[cR]

Must not have written:

w2[cR], w3[cB] since we cannot write data to disk before logging an UNDO log
