# Lecture 11

## Last time -- constructors, copy constructors

-----------------

## Destructor

- When an object is destroyed, the destructor runs.

- Sequence of events when an object is destroyed.
   1. dtor body runs
   2. dtors for fields that are objects, reverse declaration order.
   3. memory reclaimed.
  
- You got a dtor for free -- calls dtors on field that are objects.

- Sometimes the default dtor is not suitable
  ```c++
  Node *np = new Node{1, new Node{2, new Node{3,nullptr}}};
  ```
  If we allow up to go out of scoping without using delete, 3 nodes leak!
  
  Suppose we write: `delete np;`
  
  The dtor runs for `*np`
  
  The default dtor runs
  
  Node 1 has been reclaimed, Node 2 & 3 still leak!!
  ```c++
  struct Node{
      ...
      ...
      
      ~Node() {   ->Tilde followed by classname
        delete next;  ->recursive call
      }
  };
  ```


## Copy Assignment Operator

```c++
Student bobby{70,80,90};
Student billy = bobby; // copy ctor
Student jane;
jany = bobby; // copy assignment operator
```

- While we get a copy assignment operator for free, it might not be useful.

```c++
struct Node {
    ...
    ...
    Node &operator=(const Node &other) {
      data = others. data;
      delete next; // because this is an existing linked list, next could be pointing to a heap allocated node
      next = other.next? new Node(*other.next):nullptr; // call copy ctor recursively
      return *this;
    }
};
```

- This might have problems
 ```c++
 Node n {1, new Node{2,nullptr}};
 n = n; // operator=
 ```
 causes undefined behaviour: accessing/dereferencing a ptr that was deleted
 
 --> add a self reference check
 
```c++
struct Node {
    ...
    ...
    Node &operator=(const Node &other) {
      if (this == &other) return *this;
      data = others. data;
      delete next;
      next = other.next? new Node(*other.next):nullptr; // call copy ctor recursively
      return *this;
    }
};
```

- If new fials, method stops executing, next is not assigned --> next is dangling
  
  Idea: delay deleting until new has succeed
  
```c++
struct Node {
    ...
    ...
    Node &operator=(const Node &other) {
      if (this == &other) return *this; // not necessary but efficient
      Node *temp = next;
      next = other.next? new Node(*other.next):nullptr; // call copy ctor recursively
      data = others. data;
      delete temp;
      return *this;
    } 
};
```
__ALL OR NOTHING__ 
    
## Copy & Swap Idiom
```c++
#include <utility>
struct Node{
  void swap(Node &other) {
    using std::swap;
    swap(data, other.data);
    swap(next, other.next)'
  }
  
  Node &operator(const Node &other){
    Node tmp{other}; // copy ctor, temp is stack allocated
    swap(tmp);
    return *this;
  }

};
```
__Note__: no memory leak as a tmp was stack allocated, it will be destroyed; taking one old value with it.    
    
## Rvalues & rvalue reference
- Recap
  
  lvalue - something with an address
  
  lvalue reference - a const ptr with auto dereferencing; must be initialized with a lvalue
  
```c++
Node plusOne(Node n) {
  for(Node *p = &n; p; p = p->next) {     
   ++p->data;
  }
  return n;
}
  
Node n {1, new Node{2, nullptr}};
Node n2 {plusOne(n)}; // rvalue, calls the copy ctor
```
  
- Compiler creates a temporary for the returned value from plusOne

- the program
  ```
  main, n  -> 2 basic ctors
  In plusOne
    n {1,2} -> {2,3}  2 copy ctors
    temp {2,3} 2 copy ctors
  out of PlusOne
     Node n2 = tmp; 2 copy ctors
   
  We are creating a tmp to copy from and then to destroy tmp;
  ```
  What we want: should only steal if the rhs is a temporary(rvalue)
  
  - can implement a move ctor
   ```c++
   struct Node {
     Node(Node &&other) // rvalue reference
       data{other.data};
       next{other,next};{
       other.next = nullptr;
       }
   }
   ```
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
