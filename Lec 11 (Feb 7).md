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
      if (this == &other) return *this;
      Node *temp = next;
      next = other.next? new Node(*other.next):nullptr; // call copy ctor recursively
      data = others. data;
      delete temp;
      return *this;
    } 
};
```
__ALL OR NOTHING__ 
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
