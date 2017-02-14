# Lec 13

## const method
```c++
struct Student{
  int assns, mt, final;
  float grade() const {
    return assns * 0.4 +
           mt * 0.2 +
           final * 0.4;
  }
};

const Student billy{70,70,70};
billy.grade();
```

- The compiler checks that a const method does not modify fields.
- Objects that are const can only call const method.

## Mutable
```c++
struct Student{
  int numCalls;
  float grade() const {
    ++numCalls;
    return .....;
  }
};
```

- This will not compile as the function promises to not modify fields but it is modifying.
- A mutable field can be modified even for a const object.
- cosnt methods can modify mutable fields.
  ```c++
  struct Student{
    mutable int numCalls;
    float grade() const {
     ++numCalls;
     return .....;
    }
  };
  ```
  
## static

- A static field is associated with the class, not objects of the class.
- Think it as a global for the class.

```c++
struct Student {
  Static int numObjs; // declaration
  Student(----)---{
    ++numObjs;
  }
}

int main() {
  Student billy(-----);
  Student bobby{-----};
  cout << Student::numObjs << endl; // prints 2
} 
```

__Rule__: static field for a class must be defined in an external file
```c++
"student.cc"
  int Student::numObjs = 0;
```


## Static Member functions

- These are associated with the class, not objects of the class.
- You can call static member functions without on object of the class.
- static member functions do not have the `this` pointers.
- cannot access non-static fields.
- A static member function can only access static fields and call other static member functions.

```c++
struct Student {
  static int numObjs;
  static void printObject() {
    cout << "Student created:" << numObjs << endl;
  }
};
```
_(SINGLETON PATTERN: a good example, not required)_


## Invariants & Encapsulation

### Invariants
Ex:
```c++
struct Node {
  int data;
  Node *next;
  Node(int data, Node *next) :
    data{data}, next{next} {}
  __________
  __________
  __________
  ~Node() {delete next;}
};

int main() {
  Node n1{1, new Node{2, nullptr}};
  Node n2{3, nullptr};
  Node n3{4, &n2};
  ___________
  ___________
  ___________
}
```

- n1, n2, n3 are stack allocated => dtor are called
- dtor for n3 will call `delete &n2` (we are deleting something allocated on the stack)

__Class invariant:__ assumption/statement that must be true, for the class to function properly.

- Node class invariant: `next` is either a `nullptr` o a pointer returned by `new` (heap address).
- Stack class invariant: last pushed is popped first.

We need a way to prevent class invariants from being broken.

### Encapsulation

__Treat objects like black boxes__

- implementation details are hidden
- client code interacts with objects through certain selected exposed methods.

Ex1: Vector
```c++
struct Vec { // default visibility is public
  Vec(int x, int y) ......
  private: // everything that follows is not exposed to the outside world.
    int x;
    int y;
  public: // everything that follows is exposed.
    Vec operator+(...).....
};

int main() {
  Vec v{5, 6};
  cout << v.x << " " << v.y << endl; // won't compile as x & y fields are private
}
```
__Advice:__ make fields private and make selected method public.

__Keyword:__ class => __default visibility everywhere__

```c++
class Vec {
  int x;
  int y;
  public:
    Vec(int x, int y) ......
    Vec operator+ ......
```

The key idea is to create a wrapper class(list) which has exclusive access to the `Node` class.
```c++
// list.h
class List{
  struct Node; // declaration of a private nested class
  Node *thelist = nullptr;
  public:
    void addToFront(int n);
    int ith(int i);
    ~List();
};
```

```c++
// list.cc
struct List::Node {
  int data;
  Node *next;
  Node(int data, Node *next) ......
  ~Node() {......}
};

List::~List() { delete thelist;}
void List::addToFront(int n) {
  thelist = new Node{n, thelist};
}
int List::ith(int i) {
  // precondition: ith element exists
  Node *curr = thelist;
  for (int j = 0; j < i; curr = curr->next);
  return curr->data; 
  // if nullptr, clients deserve it (since they didn't follow the precondition)
}
```


































