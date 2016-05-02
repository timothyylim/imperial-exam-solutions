#Section A
### 1a

((p → q) ^ (r → s) ^ (p v r )) → (q v s)

i)


```
((¬p v q) ^ (¬r v s) ^ (p v r )) → (q v s)  

≡ ¬((¬p v q) ^ (¬r v s) ^ (p v r )) v (q v s)

≡ (¬(¬p v q) v ¬(¬r v s) v ¬(p v r)) v (q v s) (de Morgan's)

≡ (p ^ ¬ q) v (r ^ ¬ s) v (¬p ^ r) v q v s  (de Morgan's)

≡ [q v (p ^ ¬ q)] v [s v (r ^ ¬ s)] v (¬p ^ r) (commutative)

≡ [(q v p) ^ (q v ¬q)] v [(s v r) ^ (s v ¬s)] v (¬p ^ r) (distributive)

≡ [q v p v T] v [s v r v T] v (¬p ^ r)  (A v ¬A is a tautology)

≡ q v r v s v [p v (¬p ^ r)] (commutative)

≡ q v r v s v [T ^ (p v r)] (distributive)

≡ q v r v s v p v r

≡ T

```

ii)
```
 1.     ((p → q) ^ (r → s) ^ (p v r )) assume 
 2.     p → q                         1. ^E
 3.     r → s                         1. ^E
 4.     p v r                         1. ^E
 5.       p                           assume
 6.       q                           2, →E
 7.       q v s                       6, vI
 8.     p → (q v s)                   5,7,→I
 9.       ¬p                          assume
10.       r                           4,vE 
11.       s                           3,→E 
12.       q v s                       11, vI
12.    ¬ p → (q v s)                  9,12,→I
13.    (q v s)                        8,12, Dilema
14. ((p → q) ^ (r → s) ^ (p v r )) → (q v s) 1,14,→I

```

```
1.  ((p → q) ^ (r → s) ^ (p v r )) assume 
2.  p → q                           1. ^E
3.  r → s
4.  p v r 
5.    ¬(q v s)                      assume
6.    ¬ q ^ ¬ s                     lemma 1
7.    ¬ q 
8.    ¬ s
9.    ¬ p 
10.   ¬ r
11.   ¬ p ^ ¬ r 
12.   ¬ (p v r )                    lemma 2
13. q v s                          RAA 5, 12, 4

lemma 1
¬(q v s) → ¬ q ^ ¬ s 

1. ¬(q v s) assume 
2. q        assume
3. q v s    v I 
4. ¬ q      RAA 1,3

lemma 2 
¬ q ^ ¬ s →  ¬(q v s)

1. ¬ q ^ ¬ s   assume 
2. q v s       assume 
3. ¬ q         ^ E
4. s           v E, 3 
5. ¬ s         ^ E, 1
6, ¬( q v s)   RAA, 2,4,5
```

### 1b

i) 

```∀ X (p(X) →  q(X)) implies ∀ X p(X) →   ∀ X q(X)  ```
The first implies the second but the second does not imply the first so they are not equivalent. The first says "If X is a person and that person is hungry then they eat." But the second one could say "If Tim is hungry then Katie eats" because the second term is not bound by the first ∀X so they can be different people.

```
1. ∀ X (p(X) →  q(X))     assume
2. p(a) -> q(a)           ∀E, 1
  3. ∀ X p(X)             assume
  4. p(a)                 ∀E, 3
  5. q(a)                 ->E,2,4
  6. ∀ X q(X)             ∀I, 5
  7. ∀ X p(X) → ∀ X q(X)  ->I,3,6
8. ∀ X (p(X) →  q(X)) implies ∀ X p(X) →   ∀ X q(X)   ->I,1,7
```


ii)

```∃ X (p(X) ^ q(X)) implies ∃ X p(X) ^ ∃ X q(X)```
While the first implies the second, the second does not imply the first so they are not equivalent. The first says "there exists an X such that X is both, we'll say, happy and rich" but the second could say there are people who are happy and people who are rich but not necessarily both.

```
∃ X (p(X) ^ q(X))      
1. p(a) ^ q(a)                assume
  2. p(a)                     ^E, 1
  3. q(a)                     ^E, 1
4. ∃X p(X)                    ∃I, 2
5. ∃X q(X)                    ∃I, 3
6. ∃X(p(X)) ^ ∃X(q(X))        ^I, 4, 5
```

iii)

They are equivalent because: 
``` 
∀X (p(X) →  (∃Y q(X,Y) →  r(X)))
∀X (¬p(X) v  (∃Y q(X,Y) →  r(X)))
∀X (¬p(X) v  (¬∃Y q(X,Y) v  r(X)))
∀X (¬p(X) v  ¬∃Y q(X,Y) v  r(X) )
∀X (¬p(X) v r(X) v  ¬∃Y q(X,Y) )
∀X (¬(p(X) ^ ¬r(X)) v  ¬∃Y q(X,Y) )
∀X ((p(X) ^ ¬r(X)) →  ¬∃Y q(X,Y) )
∀X ((p(X) ^ ¬r(X)) →  ∀Y ¬q(X,Y) )
```

1c)
```
 1. ∀X(p(X) → q(X))       given
 2. ∀X(¬r(X) → p(X))      given
 3. p(a) → q(a)           1, ∀E
 4. ¬r(a) → p(a)          2, ∀E
 5. ¬p(a) → r(a)          4, Contraposition
       6.  ¬p(a)          assume
       7.  r(a)           5,6→E
       8.  r(a) v q(a)    7,^I
 9. ¬p(a) → (r(a) v q(a))  6,8,→I
      10.  p(a)          assume
      11.  q(a)            10,3,→E
      12.  q(a) v r(a)     11,^I
13. p(a) → (r(a) v q(a))   10,12,→I
14. (r(a) v q(a))          dilema 9,13
15. ∃X (r(X) v q(X))       14, ∃I

```
### 2 a
(i)
```
∃ X, Y [tubeline(X) ^ tubeline(Y) ^ ¬(X = Y) ^ ¬∃Z{tubeline(Z) ^ ¬(X = Z v Y = Z)}]
^ ∀ S[onNet(S) -> ∃X(tubeline(X) ^ servedBy(S,X))]
^ ∃ S,X,Y [onNet(S) ^ tubeline(X) ^ servedBy(S,X) ^ tubeline(Y) ^ ¬servedBy(S,Y)]
```
not accurate ? is the following better ? (look at the 3rd line)
```
∃ X, Y [tubeline(X) ^ tubeline(Y) ^ ¬(X = Y) ^ ¬∃Z{tubeline(Z) ^ ¬(X = Z v Y = Z)}]
^ ∀ S[onNet(S) -> ∃X(tubeline(X) ^ servedBy(S,X))]
^ ∃ S,X ∀ Y [onNet(S) ^ tubeline(X) ^ servedBy(S,X) ^ tubeline(Y) ^ ¬servedBy(S,Y)]
```


(ii)
```
∀L [ tubeline(L) → ∃S1, S2 {onNet(S1)^onNet(S2)^ S1≠S2^ servedBy(S1, L)^ servedBy(S2, L)} ] ^
∃ L1,L2,S [ posChange(L1,L2,S) <--> (onNet(S)^ servedBy(S,L1)^ servedBy(S,L2)^ L1≠L2 )]
```
more accurate ?
```
∀L [ tubeline(L) → ∃S1, S2 {onNet(S1)^onNet(S2)^ S1≠S2^ servedBy(S1, L)^ servedBy(S2, L)} ] ^
∀L1,L2,S tubeline(L1)^tubeline(L2)^¬(L1=L2)^[ posChange(L1,L2,S) <--> (onNet(S)^ servedBy(S,L1)^ servedBy(S,L2))]
```

(iii)
```
∀P,L (travel(P,L) ^ tubeline(L)) → ∃V(validtravelDoc(V,P) ∧ posses(P,V))
```

(iv)
```
∀V(validTravelDoc(V) → (dayticket(V) v seasonTicket(V) v ( freedomPass(V) ∧∃P(posses(P,V) ∧ over65(P) )
```

### 2 b
(i)
```
∀S1, S2, C (cost(S1, S2, C) ↔ cost(S2, S1, C)).
```

(ii)
```
∀S1,S2, S3, S4, C1, C2 (hub(S1),¬hub(S2),onNet(S3),onNet(S4),cost(S1,S3,C1),cost(S2,S4C2)→C1>C2)
```

### 3 a

### 3 b

```
class Property{

private:
  string name;
  List<motion_detector> detectors;
  List<guard> guards;

public:
  void assign_guard(&guard);
  void remove_guard(&guard);
  void assign_detector(&detector);
  List<guard> get_guards();
  Property(string);
}

class Motion_detector{

private:
  string location_descrption;
  Property* property;
  void send_message();

public: 
  void detect_movement();
  Motion_detector(string, property*)
}


class Guard(){

private:
  string name;

public:
  void receive(Message*);
  Guard(string);
}


class Message(){

private:
  string text;
  
public:
  Message(string);
}

```

### 3 c

```
int main(){
  
  Property *KP = new Property("Kensington Palace");
  Motion_detector *HE = new Motion_detector("Hallway East", KP);
  Motion_detector *HW = new Motion_detector("Hallway West", KP);
  Motion_detector *CJ = new Motion_detector("Crown Jewwls Display Case", KP);
  KP -> assign_detector(HE);
  KP -> assign_detector(HW);
  KP -> assign_detector(CJ);
  
  
  Property *IC = new Property("Imperial College");
  Motion_detector *RO = new Motion_detector("Rector's Office", IC);
  IC -> assign_detector(RO);
  
  Guard *Alice = new Guard("Alice");
  Guard *Bob = new Guard("Bob");
  KP -> assign_guard(Alice);
  KP -> assign_guard(Bob);
  
  HE -> detect_movement();
  
  KP -> remove_guard(Alice);
  IC -> assign_guard(Alice);
  
  CJ -> detect_movement();
  
}
```

### 3 d)

```
  void Property::assign_guard(Guard &guard){
    guards.append(guard);
  }
  
  void Property::remove_guard(Guard &guard){
    guards.remove(guard);
  }
  
  void Property::assign_detector(Motion_detector &detector){
    detectors.append(detector);
  }
  
  List Property::get_guards(){
    return guards;
  }
  
  Property::Property(string a):name(a){}
  
  Motion_detector::Motion_detector(string a, Property* b):description(a),property(b){}
  
  void Motion_detecter::detect_movement(){
    send_message();
  }
  
  void Motion_detector::send_message(){
    
    Message m = new Message(this->location_description);
    
    List<Guard> guards = property->get_guards();
    Guard g;
    
    g = guards.front();
    g.receiveMessage(m);
    
    int count = guards.size()-1;
    
    while(count > 0){
      g = guards.next();
      g.receiveMessage(m);
    }
    
  }
  
  
  
  void Message::Message(string a):text(a){}
 
```

### 4 b)

```
class Employee{

private:
  String name;
  Laptop laptop;
  
public:
  void order_laptop(int base_cost, Vector<Component> components){};
  void add_components(Laptop laptop, Vector<Component> components){};
  int get_score();
  Employee(String);
}

class Laptop{

private:
  int base_cost;
  int score;
  Vector<Component> components;

public:
  int get_base_cost(){};
  int get_no_components();
  int get_score();
  Laptop(int a, int b){};
}

class Component{

private:
  String make;
  int price;
  
public:
  get_price();
  get_score();
  Component(String, int);
}

class RAM:public Component{

private:
  int size;
  
public:
  int get_score();
  RAM(int a, int b);
}

class IO:public Component{

private:
   float response_time;

public:
  int get_score();
  IO(int a, String b, int c);
}
```

### 4 c)

```
int main(){

  Employee Andrew = new Employee("Andrew");
  
  Vector order_vector = new Vector();
  order_vector.push_back(new RAM("Crucial", 90, 8));
  order_vector.push_back(new RAM("Crucial", 90, 8));
  order_vector.push_back(new IO("Samsung", 150, 5.5));
  
  Andrew.order_laptop(500, order_vector);
  
  int score = Andrew.get_score();

  Andrew.add_component(new RAM("Corsair", 4));

  score = Andrew.get_score();

}

```

### 4 d)

```
Employee::Employee(String a):name(a){}
RAM::RAM(String a, int b, int c): size(c), Componenet(a, b) {}
IO::IO(String a, int b, int c): response_time(c), Component(a, b) {}
Component:Component(String a, int b): make(a), price(b) {}

bool Employee::orderLaptop(int a, Vector<Component> b){
  
  if (Laptop!=null) return False;
  
  int total_price = a;
  
  for (int i = 0; i < b.size(); i++){
    total_price += b[i].get_price();
  }

  if(total_price > 850) return False;
  
  Laptop laptop = new Laptop(a);
  
  for (int i = 0; i < b.size(); i++){
    laptop.components.push_back(&b[i]);
  }
  
}

int Employee::get_score(){

  if (laptop == null) return 0;
  
  int score = 100;
  
  for (int i = 0; i < laptop.components.size(); i ++){
    score += laptop.components.get_score();
  }
  
}


int RAM::get_score(){
  return size*8+price*0.1;
}

int RAM::get_price(){
  return price;
}

int IO::get_score(){
  return price*0.2+(50/response_time);
}

int IO::get_price(){
  return price;
}
```
