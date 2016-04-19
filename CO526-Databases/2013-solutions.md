### 1 a)
```
π based as iso_code,cname,net_assets (public_company⨝exchange⨝trades_on)
```
### 1 b)
```
π cname,iso_code (office) - π cname,iso_code σ office.iso_code=company.hq (company⨝office)
```
### 1 c i)
```
Shell
```
### 1 c ii)
```
SELECT cname 
FROM public_company 
EXCEPT 
SELECT cname
FROM
(
    SELECT cname, hq AS iso_code 
    FROM company
    INTERSECT 
    SELECT cname, based AS iso_code
    FROM public_company NATURAL JOIN trades_on NATURAL JOIN exchange
) AS public_companies_traded_at_hq_country
```
### 1 c iii)

```
Maybe that:

public_companies_not_traded_in_HQ_country(Cname):-
    public_company(Cname, _ , _ ),
    ¬public_traded_in_hq_country(Cname).
    
public_traded_in_country(Cname,iso_code):-
    public_company(Cname,_,_),
    trades_on(Xname,Cname,_),
    exchange(Xname,iso_code).
    
public_traded_in_hq_country(Cname,iso_code):-
    company(Cname,iso_code),
    ¬(company(Cname,iso_code),
    ¬public_traded_in_country(Cname,iso_code)).

```
###1 d i)
```
π cname, iso_code (office)
∪
π cname, based as iso_code (trades_on ⨝ exchange) 
```
###1 d ii)
```
SELECT cname, iso_code
FROM office
UNION
SELECT cname, based AS iso_code
FROM trades_on NATURAL JOIN exchange
```
###1 d iii)
```
company_listing(Cname,iso_code):-
    office(cname,iso_code).
company_listing(Cname,iso_code):-
    exchange(xname,iso_code),
    trades_on(xname,cname,_).
```

###1 e)
```
π public_company.cname (public_company)
-
(π trades_on.xname σ trades_on.cname = 'BP' (trades_on) -
π trades_on.xname σ trades_on.cname = public_company.cname (trades_on x public_company))
```
### 2 ai)
Compare all the net assets of the companies to the one with an hq in the same country and take the best.

|iso_code|cname|net_assets|
|--------|-----|----------|
|GB|BP|48914|
|US|Apple|70532|
|IE|Ryanair|2713|
|NL|Shell|142744|

### 2 aii)
```
SELECT distinct company.hq AS iso_code,
        public_company.cname,
        public_company.net_assets
FROM company JOIN public_company USING(cname)
WHERE NOT EXISTS(SELECT *
				FROM company AS same_country_company JOIN public_company AS same_country_public
				WHERE same_country_public.net_assets > public_company.assets
				AND same_country_company.hq = company.hq)
```
### 2 b)
```
SELECT distinct cname,
        COUNT(xname) as no_exchanges
FROM exchange NATURAL JOIN trades_on
GROUP BY cname
```
### 2 c)
```
SELECT hq as iso_code, 
	cname, 
	ROUND((net_assets/total_assets)*100) as pc
FROM company 
	NATURAL JOIN public_company 
	JOIN (SELECT hq as iso_code,
		SUM(net_assets) as total_assets
		FROM company NATURAL JOIN public_company
		GROUP BY hq) AS company_assets_country 
ON company.hq = company_assets_country.iso_code
```

### 2 d)
```
SELECT xname, 
	COUNT(CASE WHEN sector ='Retail' THEN cname ELSE NULL END) as no_retail,
	COUNT(CASE WHEN sector ='Oil' THEN cname ELSE NULL END) as no_oil,
FROM trades_on NATURAL JOIN company
WHERE hq = 'GB'
GROUP BY xname
```
### 2 d)
```
SELECT cname
FROM office
EXCEPT 
SELECT cname
FROM office NATURAL JOIN country
WHERE trade_block='EU' 
	OR trade_block IS NULL
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

Sc = {
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

### 4 aii)

Identify all candidate keys of R

```
CF+ = ABCDEFGH
CB gets CF so CB is also a candidate key
```

### 4 aiii)

Decompose to 3NF

```
[Not super or not prime]

Candidate keys are: CF, CB

Therefore, ADEGH are not prime since they are not in the candidate key

CBF are prime. 

Minimal cover:

Sc = {
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

A -> DEF must be decomposed as A is not a superkey and DEF are non prime

R1(A,D,E,F)

E -> G must be decomposed as E is not a superkey and G is non prime

R2(E,G)

EH -> D must be decomposed as EH is not a superkey and D is non prime

R3(E,H,D)

GH -> A must be decomposed as GH is not a superkey and A is non prime

R4(G,H,A)

Leaving 

R5(C,F,B,A)

```


### 4 a iv)

Decompose to BCNF

```
R5(C,F,B,A) violates BCNF since A is not a superkey

Decompose

R6(C,F,A)

Leaving

R7(C,F,B)

None of the FDs are lost.
```

