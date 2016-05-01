### 2 bi)

```
∀ M,A [(m(M) ^ a(A) ^ em(M,A)] ^ 
∃D [d(D) ^ ∀M(em(D,M))]
```

### 2 bii)

```
∀ C [c(C) ^ ¬sc(C) --> ∃M1, M2 (m(M1) ^ m(M2) ^ sign(C,M1) ^ sign(C,M2) ^ ¬(M1=M2) 
                       ^ ¬∃X(sign(C,X) ^ ¬(X=M1) ^ ¬(X=M2))] ^
∀ C [c(C) ^ sc(C) --> ∃D(sign(C,D) ^ d(D) ^ ¬∃X(sign(C,X) ^ ¬(X=D)]
```

### 2 biii)

```
∀ D ( d(D) ^ ∃C(c(C) ^ sign(D,C)) --> ∃M(m(M) ^ app(D,M,C)) v
∀ D ( d(D) ^ ∃C(c(C) ^ sign(D,C)) --> ∃A(a(A) ^ worksFor(A,D) ^ delegates(D,A,C) ^ ¬∃X(delegates(D,X,C) ^ ¬(X=A))
```

### 4 b)
```
class Battery{
  double max, available, rechargeP;
  
  public:
  Battery(double,double);
  void use(double);
  void recharge (double);
  double get_charge();
}

class Device{
  Battery * battery;
  
  public:
  Device(Battery*);
  virtual void operate(double) = 0;
  void recharge(double);
  double ant_life();
}

class Phone: public Device{
  int cores, tasks;
  
  public:
  Phone(Battery*, int);
  virtual void operate(double);
  void set_tasks(int);
}

class Camera: public Device{
  int consumption;
  
  public:
  Camera(Battery*);
  virtual void operate(double);
}
```

### 4 c)

```
int main(){
  Battery * b1 = new Battery(6000,500);
  Device * Canon = new Camera(b1);
  Canon->operate(1.5);
  Canon->recharge(0.5);
  cout<<Canon->ant_life();
  Battery * b2 = new Battery(4000,800);
  Device * Samsung = new Phone(b2, 2);
  Samsung->set_tasks(3);
  Samsung->operate(2);
  cout<<Samsung->ant_life();
}
```
### 4 d)

```
Battery::Battery(double a, double b):max(a),rechargeP(b){
  available = max;
}
void Battery::use(double a){ //a here is amount consumed
  if (a>available)
    available = 0;
  else
    available -= a;
}
void Battery::recharge(double t){
  if (t*rechargeP + available > max)
    available = max;
  else
    available += t*rechargeP;
}
double Battery::get_charge(){
  return available;
}

Device::Device(Battery* b): battery(b){}
void Device::recharge(double t){
  this.battery->recharge(t);
}
double Device::ant_life(){
  return battery->get_charge();
}

Phone::Phone(Battery* b, int a):Device(b),cores(a){
  tasks = 0;
}
void Phone::set_tasks(int a){
  tasks = a;
}

void Phone::operate(double t){
  if (cores>tasks)
    battery->use(tasks*t*500 + 500);
  else
    battery->use(cores*t*500 + 500);
}
Camera::Camera(Battery * b):Device(b){
  consumption = 1500;
}
void Camera::operate(double t){
  battery->use(t*consumption);
}
  
```
