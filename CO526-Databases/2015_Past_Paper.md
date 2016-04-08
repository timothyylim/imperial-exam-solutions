-------------------------------------------------------------------------------
Question 1 a)

```
π                       σ                     (airline ⋈ country ⋈ main.hub)
 aname, name, icao_code    start_year >= 1970
 ```
------------------------------------------------------------------------------- 
Question 1 b)
```
π    country - π    (airline ⋈ country)
 name           name 
 ```
-------------------------------------------------------------------------------
Question 1 c) i)

This query could also be posed as: "which airlines only fly internationally?"
```
acode
-----
AF
BA
KQ
```

-------------------------------------------------------------------------------
Question 1 c) ii)
```
SELECT acode
FROM airline
EXCEPT
SELECT acode
FROM airport AS airportA JOIN (SELECT *
                               FROM airport AS airportB
                               JOIN serves 
                               ON pcode2 = airportB.pcode) AS ports 
                         ON pcode1 = airportA.pcode 
                         AND airportA.iso_code = ports.iso_code

```
Alternative solution
```
SELECT acode 
FROM serves
EXCEPT (
	      SELECT acode
	      FROM serves JOIN airport AS airport_a ON airport_a.pcode = serves.pcode1 
	      JOIN airport AS airport_b ON airport_b.pcode = serves.pcode2 
	      AND airport_a.iso_code = airport_b.iso_code)
```

-------------------------------------------------------------------------------
Question 1 c) iii)
```
query(Acode) :-
    airline(Acode),
    ¬ subquery(Acode).
subquery(Acode),
    airport_a(Pcode1, _, Isocode, _),
    airport_b(Pcode2, _, Isocode, _),
    serves(Acode, Pcode1, _)
    serves(Acode, _, Pcode2).
    
    
```
-------------------------------------------------------------------------------
Question 1 d) i)

```
π                     flight - (π                          flight ÷ π   flight)
 acode, pcode1, pcode2           acode, pcode1, pcode2, dir          dir
```
-------------------------------------------------------------------------------
Question 1 d) ii)

```
SELECT acode, pcode1, pcode2
FROM flight AS flight_table
WHERE EXISTS (SELECT dir
              FROM flight
              EXCEPT
              SELECT dir
              FROM flight
              WHERE flihgt.acode = flight_table.acode).
```

-------------------------------------------------------------------------------
Question 1 d) iii)
```
notInAndOut(Acode, Pcode1, Pcode2) :-
    flight(_, Acode, Pcode1, Pcode2, _),
    ¬ inAndOut(Acode, Pcode1, Pcode2).

inAndOut(Acode, Pcode1, Pcode2):
    flight(_, Acode, Pcode1, Pcode2, 'O'),
    flight(_, Acode, Pcode1, Pcode2, 'I').
```
-------------------------------------------------------------------------------
Question 1 e)
```
= (A ∪ Δa) ⋈ (P ∪ Δp)
= A ⋈ (P ∪ Δp) ∪ Δa ⋈ (P ∪ Δp)  
= (A ⋈ P) ∪ (A ⋈ Δp) ∪ (Δa ⋈ Δp)  

Therefore ans = (airline ⋈ Δp) ∪ (airport ⋈ Δa) ∪ (Δa ⋈ Δp)  
```
-------------------------------------------------------------------------------
Question 2 a) i)
```
BE
```
-------------------------------------------------------------------------------
Question 2 a) ii)

Yes, EXCEPT ALL would have the effect of turning both 'SELECT acode FROM airline' and 
'SELECT flag_carrier FROM country' from sets into bags. This means that if there were duplicate 
acodes in airline and only one instance of that acode (as flag_carrier) in country then 
only one instance of acode in airline would be excluded by EXCEPT ALL. 

-------------------------------------------------------------------------------
Question 2 a) iii)
```
SELECT acode 
FROM airline
WHERE acode NOT IN (SELECT flag_carrier
                    FROM country
                    WHERE flag_carrier IS NOT null)
 ```
-------------------------------------------------------------------------------
Question 2 a) iv)
```
SELECT acode 
FROM airline
WHERE NOT EXISTS (SELECT flag_carrier
                  FROM country
                  WHERE acode = flag_carrier)
 ```
-------------------------------------------------------------------------------
Question 2 b)
```
SELECT name, 
       COUNT (CASE WHEN elevation>=1000 THEN 1 END) AS high,
       COUNT (CASE WHEN elevation<1000 THEN 2 END) AS low
FROM country LEFT JOIN airport ON country.iso_code = airport.iso_code
GROUP BY name
 ```

---

Question 4 a) i)

```
S = {A -> BCH, C -> H, D -> E, DG -> A, E -> F, EFG -> ADE, F-> E}
```

Rewrite S to an equivalent set of FDs which only have a single attribute on the RHS of each FD

```
S' = {A -> B, A -> C, A -> H, C -> H, D -> E, DG -> A, E -> F, EFG -> A, EFG -> D, EFG -> E, F -> E}
```

Simplify LHS

```
Since F -> E
EFG -> E => EG -> E
EFG -> D => EG -> D
EFG -> A => EG -> A
```

```
S'' = {A -> B, A -> C, A -> H, C -> H, D -> E, DG -> A, E -> F, EG -> A, EG -> D, EG -> E, F -> E}
or for easier reading:

S'' = {	
	A -> B, 
	A -> C, 
	A -> H, 
	C -> H, 
	D -> E, 
	DG -> A, 
	E -> F, 
	EG -> A, 
	EG -> D, 
	EG -> E, 
	F -> E	
	
}

```

Redundant FD X-> A is equivalent to the transative closure of other FDs (i.e. just cancel out transative functions)

```
Since A -> C and C -> H,
A -> H => 0

S''' = {	
	A -> B, 
	A -> C, 
	C -> H, 
	D -> E, 
	DG -> A, 
	E -> F, 
	EG -> A, 
	EG -> D, 
	EG -> E, 
	F -> E	
	
}

Since EG -> D and D -> E,
EG -> E => 0

S'''' = {	
	A -> B, 
	A -> C, 
	C -> H, 
	D -> E, 
	DG -> A, 
	E -> F, 
	EG -> A, 
	EG -> D, 
	F -> E	
}

```

---

Question 4 a) ii)

Identify and justify all candidate keys of R

```
	A -> B, 
	A -> C,
	C -> H,
	D -> E, 
	DG -> A,  
	E -> F, 
	EG -> A, 
	EG -> D, 
	F -> E	

with trial and error we can see 

D+ = ABCDEFG
Since EG -> D, EG is also a candidate key
Since F -> E, FG is also a candidate key
```

---

Question 4 a) iii)

Decompose into 3NF

```
R = {A,B,C,D,E,F,G}

Candidate keys: D, EG, FG

A,B,C are non prime 

Since DG -> A and DG is not a superkey, must decompose
R1(D,G,A)

Since A -> B and A is not a superkey, must decompose
R2(A,B)

Since A -> C and A is not a superkey, must decompose
R3(A,C)

Leaving

R4(D,E,F,G)
```

---

Question 4 a) iv)

Decompose into BCNF

_every attribute is dependent on the key, the whole key and nothing but the key_

```
R = {A,B,C,D,E,F,G}
Sc = {	
	A -> B, 
	A -> C,
	C -> H,
	D -> E, 
	DG -> A,  
	E -> F, 
	EG -> A, 
	EG -> D, 
	F -> E	}
Candidate keys: D, EG, FG

R1(D,G,A)

R2(A,B)

R3(A,C)

R4(D,E,F,G)

R4 is not in BCNF because F -> E and F is not a candidate key must decompose

R5 (F, E)

Leaving R6 (D,F,G)

Note that R2 and R3 have a common key so they can be combined to R7(A,B,C)

Finally,

R1(D,G,A)
R5(F,E)
R6(D,F,G)
R7(A,B,C)
```

