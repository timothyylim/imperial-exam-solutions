### 1 a)
```
π country.name, is_member.organization, organization.city σ (country.code = is_member.country ∧ is_member.organization = organization.abbreviation) (country ⨯ is_member ⨯ organization)
```
### 1 b)
```
πcountry.capital (country) ∪ π located.city (located)
```
### 1 c i)
```
DK 
IS 
N
---------------------
This query returns all the values in is_member which are members of all the 
organizations selected in second part of the query (i.e. organizations 
where DK is the country - i.e. NATO and NC). So DK (clearly) and IS and N 
are members of both NATO and NC so are returned.
```
###1 c ii)
```
SELECT country
FROM is_member AS compare 
WHERE NOT EXISTS (SELECT organization 
		  FROM is_member 
		  WHERE country = 'DK'
		  EXCEPT 
		  SELECT organization
		  FROM is_member
		  WHERE compare.country = is_member.country)
```
### 1 d i)

```
π country.capital σ country.code = encompasses.country  ∧ encompasses.continent = 'Europe' ∧  encompasses.percentage >= 50.00 (country ⨯ encompasses) - π city (organization)
```
### 1 d ii)
```
SELECT country.capital
FROM country JOIN encompasses ON country.code = encompasses.country
WHERE encompasses.continent = 'Europe'
AND encompasses.percentage >= 50.00
EXCEPT 
SELECT city 
FROM organization
```
### 1 d iii)
```
euro_caps(Capitals):-
	country(_,Code, Capitals, _, _),
	encompasses(Code,'Europe',Percent),
	Percent >= 50.00,
	¬organization(_,Capitals,_)).
```
### 1 e)
```
R INTERSECT S = R - (R -S) so:

π capital (country) - (π capital (country) - π city (organization)) 
```

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

To figure out if it is serializable, look for either of the following:

1. Read followed by a Write
2. Write followed by another Write

Conflicts found:

```
w3(Cis), r1(Cis) 
r1(Cfl), w3(Cfl) 
```

Waits for graph:

```
T3 ---> T1
^	     |
|--------
```

Cycle, shit.

This causes a deadlock since T3 is holding ```wl1(Cis)``` but T1 is holding ```rl2(Cfl)```.

Recoverability:

T1 reads T3 transactions before T3 commits. This is a dirty read, bad T1.

However since T1 commits after T3 and T3 writes data but does not depend on T1, the concurrent execution is recoverable, but not ACA or ST.

### 3 biii)

Conflict pairs:

```
w3(Cis) <--> r1(Cis)
r1(Cfl) <--> w3(Cfl)
```

It comes down to who acquires the read/write lock for Cis first.

If T3 acquires it first, T1 will be delayed until after T3 commits (and thus releasing all its locks), and T3 would not need to wait for T1 for lock on Cfl.

If T1 acquires it first, then T3 would be delayed until after T1 commits, and T1 would not need to wait for lock on Cfl either.

T1 and T3 could never deadlock.

### 3 biv)

Conflict pairs between T1, T2 and T3:

```
r1(cCh) <-> w2(cCh)
r1(Cis) <-> w3(Cis)
r1(Cn) <-> w2(Cn)
r1(cfl) <-> w3(cfl)
```

Consider the following execution:

```
r1(cch),
r1(cis),
r2(cn),
w2(cn),
w3(csf),
r2(cs),
w2(cs),
r2(cch)
```

T1 holds ```rl1(cch)```

T2 holds ```wl2(cn)```

T3 holds no relevant locks

waits for graph:

```
   T2 -- wl2(cch) --> T1 <--- wl3(cis) -- T3
   ^                  |
   |-----rl1(cn)-------

```




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

