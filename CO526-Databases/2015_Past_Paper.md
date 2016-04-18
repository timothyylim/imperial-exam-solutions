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

Alternative answer: I think it asks for airlines that don't fly locally (so they could fly both locally and internationally and I don't think they would appear).
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

I *think* serves needs to be at the top of the subquery since Acode is ground. That way, Pcode1 and Pcode2 are ground for the airport_a and airport_b calls unless that is just prolog nonsense. I could be wrong. -KS

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
S = {
	A -> BCH,
	C -> H,
	D -> E,
	DG -> A,
	E -> F,
	EFG -> ADE,
	F -> E
}
```

Rewrite RHS to only have one attribute

```
S = {
	A -> B,
	A -> C,
	A -> H,
	C -> H,
	D -> E,
	DG -> A,
	E -> F,
	EFG -> A,
	EFG -> D,
	EFG -> E,
	F -> E
}
```

Simplify LHS

```
Since E -> F,
EFG -> A => EG -> A
EFG -> D => EG -> D
EFG -> E => EG -> E


S' = {
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

Find minimal cover using transitivity

```

```

---

Question 4 a) ii)

Identify and justify all candidate keys of R

```

```

---

Question 4 a) iii)

Decompose into 3NF

```

```

---

Question 4 a) iv)

Decompose into BCNF

_every attribute is dependent on the key, the whole key and nothing but the key_

```

```

---

Question 4 b) i)


---

Question 4 b) ii)

Steps to recover a database:

- Find set of commited transactions, uncommited transactions and list of undo actions
- Actions to be undone before cp record
- Actions to be redone after cp record

- Find set of commited transactions, uncommited transactions and list of undo actions:

```
C = {1,2}
I = {3,1}
UNDO w1[aKQ, no_aircraft = 55]
UNDO w3[aBA, no_aircraft = 297]
```
- Actions to be undone before cp record

```
cp-C={3}
UNDO w3[aAF, no_aircraft = 242]
```

- Actions to be redone

```
All in C after cp

REDO w1[aKQ, no_aircraft = 56]
REDO w2[aKQ, no_aircraft = 57]
```

Finally
```
AF = 242
KQ = 57
```
