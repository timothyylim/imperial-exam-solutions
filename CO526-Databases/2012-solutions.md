

### 2 c)
```
select distinct continent,
	SUM(area) as total_area
from (select continent, 
		encompasses.percentage * country.area as area
	from encompasses JOIN country
	on country = code) as fuck
group by continent
order by total_area asc
```

### 2 di)
```
select organization, city
from 	(select organization,
		COUNT(CASE when continent='Europe' then continent else null end) as eur_member,
		COUNT(CASE when continent='Africa' then continent else null end) as af_member,
		COUNT(CASE when continent='Asia' then continent else null end) as asian_member
	from is_member JOIN encompasses ON is_member.country = encompasses.country
	where percentage > 50
	group by organization) join organization 
ON organization.abbreviation = is_member.organization
```
### 2 dii)
Just add :
```
where eur_member > 0
```

Not sure, couldn't test it.


### 3 bi)


To figure out if it is serializable, look for either of the following:

1. Read followed by a Write
2. Write followed by another Write

Only conflicts found:

```
w3(Cis), r1(Cis) 
w3(Cfl), r1(Cfl) 
```


waits for graph:

```
T3 --> T1
```

No cycle, nice!

We can see that it is serializable (CSR).

And for recoverability, consider if the commits depend on anything:

The commit ```c1``` depends on ```w3(Cis)``` and ```w3(Cfl)```, (which are not yet committed) and is therefore not recoverable due to dirty read.


### 3 bii)



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


Minimal Cover 

```
Sc = {
      AB  -> C,
      AB  -> E,
      GH  -> E,
      E   -> F,
      D   -> B,
      C   -> A,
      C   -> D
}
```

### 4 aii)

Identify and justify all candidate keys of R

```
CGH+ = GHEFADBC

GHAB is also a candidate key as AB -> C
```

### 4 aiii)

Decompose to 3NF

[non super, non prime]

Non prime: DEF
Prime: ABCGH


```
Decompose E -> F since E is not super and F is not prime

R1(E,F)

AB -> E since AB is not a superkey and E is not prime 

R2(A,B,E)

GH -> E since GH is not a superkey and E is not prime

R3(G,H,E)

C -> D since C is not a superkey and D is not prime

R4(C,D)

Since we are losing a functional dependency D -> B, we add it back in

R5(D,B)

Leaving

R6(A,B,C,G,H)

```


### 4 a iv)

Decompose to BCNF

```
{
      AB  -> C,
      C   -> A,
}

replace R6 = R6(A,B,C)

R7(A,B,G,H)

No FD lost.
```

### 4 bi)

Backward scan:

Undo log for transactions in c and objects in D

Undo all logs for objects not in D

| log  | action    |
|---|----|
| ...  | c = {}, D = {}    |
| w3[cUsa, pop = 268 539 881 ]| undo as cUSA is not in D       |
| w1[cUsa, pop = 268 467 239 ]| undo as cUSA is not in D       |
| b3				| irrelevant       |
| c2				| c = {2} |
| w1[cAus, pop = 19 284 997]  	| undo as cAus is not in D |
| w2[cSf, pop = 5 105 230]  	| no action, D = {Sf} |
| w2[cUsa, pop = 266 476 278]  	| no action, D = {Sf, USA} |
| w2[cAus, pop = 18 260 863]  	| no action, D = {Sf, USA, Aus} |
| b2 	| irrelevant|
| w1[cSf, pop = 509672]		| no action as cSf is in D |
| w1[cFl, pop = 31 122]		| undo as Cfl is not in D |


After recovery:

|code|population|
|----|---|
|Aus | 19284997|
|Fl | 31122|
|Sf | 5105230|
|USA|26847239|

