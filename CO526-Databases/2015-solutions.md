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

-------------------------------------------------------------------------------
Question 3 a) [Diagram](https://github.com/timothyylim/imperial-exam-solutions/blob/master/CO526-Databases/db2015.pdf).  There is also a version that can be edited in the Databases folder (powerpoint).

-------------------------------------------------------------------------------
Question 3 b) 

-------------------------------------------------------------------------------
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
Since A -> C, C -> H
A -> H => 0

Since EG -> D, D -> E
EG -> E => 0

Minimal cover
Sc = {
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
I'm pretty sure you can remove EG -> A as well because if you remove it, EG+ is still ABCDEFGH. -KS

---

Question 4 a) ii)

Identify and justify all candidate keys of R

```
EG+ = ABCHDEFG

So EG gets everything.

Note nothing gets G, so G has to be in the candidate key.

FG gets EG, so FG is also a candidate key.

DG gets EG, so DG is also a candidate key (note D -> E).

Therefore,

EG, FG, DG are candidate keys.
```

---

Question 4 a) iii)

Decompose into 3NF

```
Candidate keys: EG, FG, DG.

Thus ABCH are non prime since they are not in the candidate keys.

EDFG are prime.

Minimal cover
Sc = {
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


Since C is not a superkey and H is non-prime, 
C -> H must be decomposed

R1(C,H)

Since A is not a superkey and BC are non-prime,
A -> BC must be decomposed

R2(A,B,C)

Leaving 

R3(A,D,E,F,G)

```

---

Question 4 a) iv)

Decompose into BCNF

_every attribute is dependent on the key, the whole key and nothing but the key_

```
From 3NF:
R1(C,H)
R2(A,B,C)
R3(A,D,E,F,G)

Since E is not a super key, decompose E -> F (F -> E is also taken out)

R4 (E,F)

Since D is not a super key, decompose D -> E

R5 (D,E)

Leaving:

R6 (G,A,D)

Can't combine any relations as none share a common key.

We lost EG -> AD. It seems you cannot keep this FD. 

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