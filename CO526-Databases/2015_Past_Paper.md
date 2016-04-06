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
'SELECT flag_carrier FROM country' into sets. This means that if there were duplicate 
acodes in airline and only one instance of that acode (as flag_carrier) in country then 
only one instance of acode in airline would be excluded by EXCEPT ALL. 

-------------------------------------------------------------------------------
Question 2 a) iii)
```
SELECT acode 
FROM airline
WHERE acode NOT IN (SELECT flag_carrier
                    FROM country)
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


 





