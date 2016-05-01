### 2 ai)

```
∀ D,C [reg(C) ^ dir(D,C) ^ ¬∃D2( reg(C) ^ dir(D2,C) ^ ¬(D2=D1)]
```

### 2 aii)

like an 'if else' statement

```
∀ ID,C,D,S [reqReg(ID, C, D, S) --> {(reg(C) v disq(D) v S < 5000) --> reject(ID)} 
    ^ {¬(reg(C) v disq(D) v S < 5000) --> accept(ID)}]

```


### 2 aiii)

```
∀ D {[∃ C (dir(D,C) ^ reg(C) ^ insolvent(C)] --> 
            disq(D) ^ [∀ C (reg(C) ^ dir(D,C) --> ∀ V (share(C,V) ^ V = 0)]}
```


### 2 aiv)

```
For all Directors, Companies and Periods (if a director is a director of C and not disqualified and
                                          there exist two different failures to do the accounts
                                          then warn the director)
```

```
∀ Dir, C, P (dir(Dir,C) ^ ¬disq(D) ^ 
            ∃ D1,D2(acc_due(C,P,D1) ^ ¬acc_done(C,P,D1) ^ acc_due(C,P,D2) ^ ¬acc_done(C,P,D2) ^ ¬(D1 = D2)) 
            -->
            warn(D,C))
```


### 3 b)

```
class bicycle{

private:
  int frame_id;
  
  

}
```


### 3 c)

