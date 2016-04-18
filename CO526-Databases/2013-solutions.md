### 1 a)

```
π iso_code, cname, net_assets (company ⨝ office ⨝ public_company)
```
### 1 b)
```
π cname, iso_code (company ⨝ country) - π cname, iso_code σ company.hq = country.iso_code (company ⨝ country)
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
Not sure if correct:

public_companies_not_traded_in_HQ_country(Cname):-
    public_company(Cname, _ , _ ),
    ¬public_traded_in_hq_country(Cname).
    
public_traded_in_hq_country(Cname):-
    company(Cname,HQ,_),
    public_company(Cname,_,_),
    trades_on(Xname,Cname,_),
    exchange(Xname,HQ).


```
###1 d i)
```
π company.cname, company.hq (company)
∪
π company.cname, exchange.based σ  company.cname = trades_on.cname ∧ trades_on.xname = exchange.xname (company ⨯ trades_on ⨯ exchange) 
```
###1 d ii)
```
SELECT cname, hq
FROM company
UNION
SELECT trades_on.cname, exchange.based
FROM trades_on JOIN exchange ON exchange.xname = trades_on.xname
```
###1 d iii)
```
links_to_country(Cname,Isocode):-
    company(Cname,Isocode,_)
    ;
    trades_on(Xname,Cname,_),
    exchange(Xname, Isocode).
```

###1 e)
```
π public_company.cname (public_company)
-
(π trades_on.xname σ trades_on.cname = 'BP' (trades_on) -
π trades_on.xname σ trades_on.cname = public_company.cname (trades_on x public_company))
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

