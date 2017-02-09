# Lec 10
## Last Time
      - C++ Classes
      - Constructions
      
```c++
      Struct Student {
           int assns, mt, final;
           Student(int assns = 0, int mt = 0, int final = 0)
           {    this->assns = assns < 0? 0 : assns;
                this->mt = mt < 0? 0 : mt;
                this->final = final < 0 ? 0 : final;
                }
           };
           
       Student bobby{80, 70, 70};
       Student billy{80, 70};
       Student newguy{}; // Student new guys;
```

Built-in/Default Constructor;

Every calss comes with a default constructor - calls default constractors on fields that are objects

Has no parameters

```
Struct A{
     int x;
     Student s;
     Student *p;
}


A myA;   Primitive types/pointers are not initialized to default value

*(myA.p) (incorrect);
```

***myA.s can be accessed, myA.s.assns's value isn't necessairly the default value***

***Rule: the default constructor goes away as soon as you write any constructor***

```
Vec v; // decault constructor called and will be compiled

struct Vec{
     int x;
     int y;
     Vec(in x, int y) {
           this -> x = x;
           this -> y = y;
          }
      };
```

***After the specific constructor is defined, Vec v will not be compiled and Vec v{1,2} works***

How to initialize fileds that are constant and (references)

```
Struct Mystruct{
     const int myconst - 5;
     int &myRef = m;
    }
```

All objects will have myConst set to 5 and myRef a reference to m

```
struct Student {
   const int id = 20233118;
   .
   .
   .
  };
```
We might not want all objects to have the same const / ref value
-cannot do in class initialization
  
Can we do it in the constructor body?
No!!!

fields must already be constructed before the constructor body runs

Steps when an obejct is created
1. Space is allocated
2. fields initialization: default constructors for fields that are objects
3. Constructor body runs

Since step 3 is too late, hijack step 2
Use; Members Initialization List (MIL)

struct Student {
      int assns, mt, final;
      const int id;
      Student(int assns; int mt; int fianl; int id)
         : assns{assns}, mt{mt}, final{final}, id{final}
         { constructor body }
      };
      
- MIL syntax is reserved for constructor
- MIL can be used to initializeall fields (not just consts/refs)
- You should use the MIL whenever's possible
  MIL can be more efficient
- In an MIL, do not need "this" to differentiate between fields and parameters with the same name;
- MIL always initialize fields in declaration order

```
Struct Vec {
     int x = 9;
     int y = 9;
     Vec(int x, int y) : x{x}. y{y} {}
};  Remark: this->X will have the value given in the parameters, default value is overridden

Student bobby{70,70,70};
Student billy{bobby}; //Student billy = bobby;

billy is a copy of bobby

To create an object as a copy of another object, the copy constructor is called
      - You get one for free
      - field for field copy
      
Every calss comes with
      - default constructor (0 parameters) give away if you write any constructors
      - copy constructor
      - destructor
      - copy assignment operators
      - move constructor
      - move assignment operator
      
Struct Student{
       int assns, mt, final;
       
       Student(const Student &othes)
           : assens{others.assns}, mt{others.mt}, final{others.final}
           {}
       }: (get this for free)
       
Struct Node {
      int data;
      Node *next;
      Node (int data,　Node*next):data{data}, next{next}{}
      Node (const Node &others):
            data{others.data},next{others.next}{}
      };
      
Node *np = new Node{1,new Node{2, new Node{3, empty}}};

Node m = *np // copy constructor
Node *p = new Node(*np); // calls copy constructor

Default copy constructors do a shallow copy
If you want a deep copy, you need to write your own copy constructor

Struct Node{
       Node(const, Node&others){
             data = others.data
             if (others.next == nullptr)
                   next = nullptr;
             else 
                   nexr = new Node(*others.next);
             }
        };(correct but long)
        
Struct Node {
        .
        .
        .
        Node (const Node &others) :data{other.data}
             next{ other.next? new Node(*other next) : nullptr}{}
        };
 ```
 
 Places where a copy constructor is called
 
      - when an object is created as a copy of anothers;
      - pass by value
      - return by value
      
The copy constructor must be a ference

Aside  single parametor constructor
```

Struct Node{
       int data;
       Node *next;
       Node(int data) : data{data}, next{nullptr}{}
};

void foo(Node n) {.......}  create impicit conversion

Node n{4}; (correct)
Node n = 4; (correct)
foo(4); correct

You can disallow automatic conversions by using the "explicit" keyword

Struct Node{
       int data;
       Node *next;
       explicit Node(int data) : data{data}, next{nullptr}{}
};

Node n(4); (correct)
Node n = 4; (incorrect)
foo(4); (correct)
```

Destructor

      - stack allocated object goes out of scope
      - heap "            " delete is called
        Objects are destroyed by running distructors
        
You get one for free

When an object is destroyed:
1. destructor body runs
2. destructor for fields run, reverse declaration orders
3. space deallocated
