### 1 ai)

```
∃ X, Y (day(X) ^ evening(Y))
```

### 1 aii)

```
∀ P, C [(teaches(P,C) ^ day(C) ^ (¬∃C2 teaches(P,C2) ^ eve(C2)) --> salary(P,sd)] ^
∀ P [∃C1,C2(teaches(P,C1) ^ teaches(P,C2) ^ day(C1) ^ evening(C2)) --> salary(P,sde)] ^
∀ P, C [(teaches(P,C) ^ evening(C) ^ (¬∃C2 teaches(P,C2) ^ day(C2))) --> salary(P,se)]  
```

### 1 aiii)
```
∀C,Sub [eve(C) ^ subject(Sub,C) -> type(Sub,'languages') v type(Sub,'humanities')] ^
∃C,Sub [day(C) ^ subject(Sub,C) -> type(Sub,'languages') v type(Sub,'humanities')] ^
¬∃C subject('Latin,C) ^ (day(C) v eve(C))
```

### 1 aiv)
```
∀S,C,Sub [enrolled(S,C) ^ day(C) ^ subject(Sub,C) -> sitExams(S,Sub) ] ^
∀S,C,Sub [(enrolled(S,C) ^ subject(Sub,C) -> eve(C)) -> ¬sitExams(S,Sub)]
```

```
Not sure second half of above is correct: "but no one enrolled on evening classes only will sit any examinations" 
enrolled in evening classes and not enrolled in day classes -> not sit exams

∀S,C,Sub [enrolled(S,C) ^ day(C) ^ subject(Sub,C) -> sitExams(S,Sub) ] ^
∀S,C,Sub [ ∃C(enrolled(S,C) ^ subject(Sub,C) ^ eve(C)) ^ ¬∃C(enrolled(S,C) ^ subject(Sub,C) ^ day(C)) -> ¬sitExams(S,Sub)]
```



### 1 b)

**(i.)** S1 and S4
```
AXAT(e(X,T) ^ ¬p(X,T) -> s(X,T))    given
AXAT(¬(e(X,T) ^ ¬p(X,T)) v s(X,T))  implication
AXAT(¬e(X,T) v ¬¬p(X,T) v s(X,T))   deMorgan's
AXAT(¬e(X,T) v p(X,T) v ¬¬s(X,T))   double negation (twice)
AXAT(¬¬s(X,T) v (¬e(X,T) v p(X,T))) associative
AXAT(¬s(X,T) -> (¬e(X,T) v p(X,T))) implication
```

### 2 a)

```
    1. ¬(p,q)               assume
        2. ¬(¬pv¬q)         assume
            3.¬p            assume
            4.¬pv¬q         3,vI
        5.p                 2,4,RAA
            6.¬q            assume
            7.¬pv¬q         6,vI
        8.q                 2,6,7,RAA
        9. p,q              5,8,^I
    10. (¬pv¬q)             1,2,9,RAA
11. ¬(p,q) → (¬pv¬q)        1,10,→I
    12. (¬pv¬q)             assume
        13. (p,q)           assume
        14. p               13,^E
        15. ¬¬p             14, ¬¬I
        16. ¬q              12,15,^E
        17.  q              13,^E 
    18. ¬(p,q)              13,16,17
19. (¬pv¬q) → ¬(p,q)        12,18,→I
20. (¬pv¬q) ↔ ¬(p,q)        11,19,↔I
```

### 2 b)

```
    1. m(a) ^ p(a)                      assume
    2. p(a)                             1, ^E
    3. p(a) -> ¬(q(a) ^ r(a))           S1, ∀E
    4. ¬(q(a) ^ r(a))                   2,3,->E
    5. m(a)                             1, ^E
    6. m(a) -> ∃Y s(a,Y) v ∃Y t(a,Y)    S3, ∀E
    7. ∃Y s(a,Y) v ∃Y t(a,Y)            6,->E
        8. ¬(∃Y t(a,Y))                 assume
        9. ∃Y s(a,Y)                    7,8,vE
        10. ∃Y s(a,Y) -> q(a)           S2, ∀E
        11. q(a)                        9,10, ->E
        12. ¬(n(a) ^ r(a)) -> ∃Y t(a,Y) S4, ∀E
        13. n(a) ^ r(a)                 8, 12, Modus tollens
        14. r(a)                        13, ^E
        15. q(a) ^ r(a)                 11,14,^I
    16. ∃Y t(a,Y)                       15, 4, 8, RAA
    17. m(a) ^ p(a) -> ∃Y t(a,Y)        1,16, ->I
    18. ∀X (m(X) ^ p(X) -> ∃Y t(X,Y))   17, ∀I
```

### 2 c)

```
    1. ¬∃Y u(a,Y)                       assume
    2. ∀Y ¬u(a,Y)                       equivalent, 1
    3. ¬u(a,b)                          2, ∀E
    4. t(a,b) -> u(a,b)                 S5, ∀E
    4. ¬t(a,b)                          3,4,Modus tollens
    5. ∀Y ¬t(a,Y)                       4,∀Y
    6. ¬∃Y t(a,Y)                       5, equivalent
    7. m(a) ^ p(a) -> ∃Y t(a,Y)         past question, ∀E
    8. ¬(m(a) ^ p(a))                   6,7, Modus tollens
    9. ¬∃Y u(a,Y) -> ¬(m(a) ^ p(a))     1,8,-> I
    10 ∀X(¬∃Y u(X,Y) -> ¬(m(X) ^ p(X))) 9,∀I
```

### 3 a)

### 3 b)

```
class User{

private:
  float x;
  float y;
  Position p;
  int credits;

public:
  broadcast(Position p; String t, int r);
  update_position(Position p);
  buy_credits(int c);
}


```

### 3 c)

```
List<User> directory = new List();

User *Alice = new User(3.5,0,5,5);
User *Bob = new User(10.0,5.0,0);
User *Charles = new User(7.0,7.0,2);

directory.append(Alice);
directory.append(Bob);
directory.append(Charles);

Alice.broadcast("Hello",10,directory);
Alice.update_position((3.0,3.0));

cout << Alice.get_credits();

Charles.broadcast("Come to my..",5,directory);

Bob.buy_credits(10);
```

### 3 d)

```
User::User(int a, int b, int c):x(a),y(b),credits(c){};

void User::broadcast(String a, int b, List<User> c){
  
  if (credits < 1) return;
  if (c.size() == 0) return;
  
  String message = a;
  int radius = b;
  
  x2 = c.front().x;
  y2 = c.front().y;
  
  //if radius is in range broadcast
  
  while (c.next() != null){
    // if radius in range, broadcast
  }
  
}

void User::buy_credits(int a){
  credits += a;
}

int User::get_credits(){
  return credits;
}
```

### 4 b)
```
class Car{

private:
  String model;
  int mass;
  Chassis c;
  Engine e;
  
public:
  int calc_mass();
  int calc_time();
  Car(String, Chassis, Engine, int){};
  
}

class Chassis{

private:
  int mass;
}

class Engine{

private:
  int mass;
  int power_factor;
  int number_of_cylinders;

}

class Driver{

private:
  int mass;
  String name;
  
public:
  Driver(String name, int mass){};
}




```

### 4 c)

```
int main(){

  Driver LH = new Driver("Lewis Hamilton", 67);

  Car NR = new Car("NR-14", new Chassis(582), new Engine(5, "Turbo...", 91, 250));
  
  Car TF = new Car("TFD-2", new Chassis(411), new Engine(4, "Super...", 87, 175));
  
  cout << NR.calc_time(LH, 1000, 642);
  
  cout << TF.calc_time(LH, 1500, 642);
  
  cout << NR.calc_time(LH, 1000, 550);
  
  cout << TF.calc_time(LH, 1500, 550);
  
}

```

### 4 d)

```
Driver::Driver(String a, int b):name(a),mass(b){};

int Driver::get_mass(){return mass};

Car::Car(String a, Chassis b, Engine c, int d):model(a),Chassis(b),Engine(c),mass(d){};

int Car::calc_time(Driver driver, int distance, int max_weight){
  
  int total = driver.get_mass() + chassis.get_mass() + engine.get_mass()
  
  if (total > max_weight) {return 0;}
  
  else{ total += (max_weight-total);}
  
  if( model = "Turbo"){return output of the fucking turbo equation;}
  
  if( model = "Super"){return output of the fucking turbo equation;}
  
  return 0;
}
```
