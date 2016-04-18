### 2 c)

select distinct continent,
	SUM(area) as total_area
from (select continent, 
		encompasses.percentage * country.area as area
	from encompasses JOIN country
	on country = code) as fuck
group by continent
order by total_area asc



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
