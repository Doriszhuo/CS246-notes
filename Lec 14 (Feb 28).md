```
// list.h

class List {
  struct Node; // private nested class
  Node *theList = nullptr;
public:
  void addToFront(int n);
  int ith(int i);
  ~List();
  // ... etc etc
};

// list.cc
#include "list.h"
struct List::Node {
  // nested class
  int data;
  Node *next;
  Node(int d, Node *n): { // MIL

  }
  ~Node() {
    delete next;
  }
};

void List::addToFront(int n) {
  theList = new Node(n, theList);
}

int List::ith(int i) {
  Node *cur = theList;
  for (int j = 0; j < i; j++) {
    cur = cur->next;
  }
  return cur->data;
}

List::~List() {
  delete theList;
}
```

Traversal is O(n^2)

###Design Patterns###

If you have "this kind of" problem, then "this programing technique" solves it

**Iterator Pattern**

- Still not going to expose Nodes

- Create a class that manages Nodes and allows us to walk the linked list (Class Iterators)

Inspiration: array traversed using patterns

```
// arr is an array

for ( int *p = arr; p != arr+n; ++p){        
  ..................*p.............. (derefference)
  }
  
arr: start 
!=:not equal  
arr+n: one past the end  
++p:prefix operator
```

**Todo List for List Iterator**

- operator ++ (prefix operator)
- operator * (dereference)
- !=, ==
- a way to indicate the begin and end

```
Class List{
   struct Node;
   Node *theList;
   public:
    class Iterators{
           Node *p;
           public:
           explicit Iterator(Node *p) : p{p}{}
           int operator*() const {
                  return p->data;
                }
           Iterator& operator++() {
                     p = p->next;
                     return *this;
           }
           bool operator==(const Iterator &other){
                return p == other.p;
           }
           bool operator!=(const Iterator &others){
                 return !(*this == other)   note: call operator==
           }
     };//endclassIterator
     
   Iterator begin(){ return Iterator{thelist};}
     
   Iterator end() { return Iterator{nullptr}; }
 };
```

```
  int main() {
      List lst;
      lst addToFront(1);
      lst addToFront(2);
      int addToFront(3);
      
      for (List::Iterator it = lst.begin(); it != lst.end(); ++it)
      {
            cout << *it << endl;
      }
          O(n) traversal
```

***Automatic Type Inference (auto keyword)***

auto x = y; // x is defined to be the same type as y

```
for (auto it.lst.begin(); ......)
}
```

__C++11 supports range-based for loops__

```

for(auto n : lst){
    cout << n << endl;　         n will contain copies of int data in each iterration
}

for (auto &n : lst) {
       //n is a reference to actual data fields in the linked list
}
```

To use a range based for loop (eg: Listclass) for class C

1. Class C must have methods begin & end, which return iterator

2. The Iterator class must implement operator*. operator++, operator!=


Problem: constructor of iterator class is public, which means client code might create their own iterator
      auto it = Iterator{nullptr};
      
We want to force client code to use begin and end (not create their own)

Idea: make Iterator constructor private

__But then no one (not even List class) can construct Iterator objects__

__Iterator can make the list class a friend__

```
  class List{
      ...
      ...
      public:
      class List{
           node *p
           explicit iterator(node *p) : p{p}{}
           public:
           
           friend class list;
        };
    };
```

Making a class a "friend" gives the class full access to everything that was private

-- Make as few friends as possible because friendship breaks encapsulation

Keep fields private, provide accessors or mutators as needed

```
class Vec {
     int x, y;
     public:
       int getX() const {return x;}
       int gety() const {return y;}
       void setx(int v) { x = y; }
       void sety(int y) { y = x; }
    };
```

Suppose I have the vec class 
          - private fields
          - No getX and get y
But I want to implement operator<< for Vec

Recall operator<< is implemented as a function
      - how do I gain access to value of x and y
      
```
Class Vec{
     int x, y;
     public:
     friend std::ostream &operator<<(std::ostream &out, const Vec &v);
     operator << has access to x and y
```

**System Modelling**

- Better to design in advance how classes interact with each others

UML: Unified Modelling Language

 Modelling a class in UML  
 
 ```
 + means public, - means private
 
 [Vec] <- class name
 [ - x:Integer ] <- fields (optional)
 [ - y:Integer ]     
 [ + Vec();    ] <- methods (optional)
 [ + operator+ ] 


Relationship 1: Composition

class Vec{
      int x, y;
      public:
      Vec (int x, int y) : x{x}, y{y}{}
      
class Basis{
      Vec v1, v2;
      public:
   }
   
int main(){
    Basis b;
 } (won't compile)
 
 class "Basis"{
        Vec v1, v2;
        public:
        Basis()　: vec{1,0}, v2{0,1}{}
     };
     Basis b; (now will compile)
