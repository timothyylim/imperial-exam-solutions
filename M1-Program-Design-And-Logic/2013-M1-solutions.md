### 2 ai)

```
∀ D,C [reg(C) ^ dir(D,C) ^ ¬∃D2( reg(C) ^ dir(D2,C) ^ ¬(D2=D1)]
```
Alternative
```
∀C [reg(C) --> ∃D[dir(D,C) ^ ¬∃B(dir(B,C) ^ ¬∃B(dir(B,C) ^ ¬(B=D))]]
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
Alternative
```
∀D,∀C [ (
         reg(C) ^ dir(D,C) ^ ¬disq(C) ^
         ∃D1,∃D2 [  
                  ∃P,∃D (acc_due(C,P,D) ^ acc_filed(C,P,D1) ^ (D1>D)) ^   
                  ∃P,∃D (acc_due(C,P,D) ^ acc_filed(C,P,D2) ^ (D2>D)) ^ 
                  ¬(D1=D2)
                 ]
        )
        --> ward(D,C) ]
```
### 3 a)

```
class Bike{
    string frame;
    string make;
    double price;
    public:
    Bike(string, string, double);
    double get_price();
}

class Shop{
    Table<Bike*, int> myTable;
    
    public:
    bool sell(Bike*);
    void service(Bike*);
    void past_services(Bike*);
    Shop();
}

class Customer{
    double account;
    string name;
    Bike* bikes[10];
    int b; //number of bikes;
    
    public:
    Customer(string);
    void deposit(double);
    bool buy(Bike*, Shop*);
}
```

### 3 b)

```
int main(){
    Customer* lance = new Customer("Lance");
    lance->deposit(2000);
    Bike* b1 = new Bike("TK15895", "Trek", 475);
    Bike* b2 = new Bike("SS82300", "specialised", 1600);
    Shop* sh = new Shop();
    lance->buy(b1,sh);
    lance->buy(b2,sh);
    lance->service(b1,sh);
    lance->service(b2,sh);
}

```
### 3 c)

```
Shop::Shop(){}
bool Shop::sell(Bike*){
    if(myTable.get(Bike) == null){
        myTable.set(Bike, 0);
        return true;
    }
    return false;
}

void Shop::service(Bike*){
    int* c = list.get(Bike);
    list.set(Bike, ++(*c));
}

int* Shop::past_service(Bike* b){
    return myTable.get(b);
}

Bike::Bike(string a, string b, double c):frame(a),make(b),price(c){}
double Bike::get_price(){
    return price;
}

Customer::Customer(string a):name(a){
    account = 0;
    b = 0;
}
void Customer::deposit(double a){
    account += a;
}
bool Customer::buy(Bike* b, Shop* sh){
    int price = bike->get_price();
    if(price>account)
        return false;
    account -= price;
    sh->sell(Bike);
    bikes[b] = Bike;
    b++;
}
bool Customer::service(Bike* bike, Shop* sh){
    int* price = sh->past_services(bike);
    int cost;
    if(*price == -1)
        return false;
    else if(*price > account)
        return false;
    else if(*p == 0)
        cost = 0;
    else if(*p == 1)
        cost = 20;
    else 
        cost = 40;
    account -= cost;
    sh->service(bike);
}

```

### 4b)

```
class Competitor{

    private:
        String name;
        int age;
    
    public:
        Competitor(String, int);
        compete(Event *, int);
        compute();
}

class Event{

    protected:
        double a,b,c;
    
    public:
        Event(double,double,double);
        virtual double score(double) = 0;
}

class Run{

    public:
        Run(double,double,double);
        virual double score(double);
}


class Jump{

    public:
        Jump(double,double,double);
        virual double score(double);
}

class Throw{

    public:
        Throw(double,double,double);
        virual double score(double);
}


```

### 4c)

```
int main(){

    Event* 100m = new Run(9.23, 26.7, 1.835);
    Event* high = new Jump(1.85, 75, 1.348);
    Event* shot = new Throw(56.02,1.5,1.835);
    
    Competitor JE = new Competitor("Jessica Ennis", 28);
    
    JE -> compete(100m,12.54);
    JE -> compete(high,186);
    JE -> compete(shot,14.28);
    
    cout >> JE -> compute();
}
```

### 4d)


```

```
