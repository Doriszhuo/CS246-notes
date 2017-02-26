# Lecture 7
## Last time
- Short topics
- Default Arguments
- Function Overloading
- Structs
- Constants

-----------------------

## Parameter Passing
```c++
void inc(int n) {n = n + 1;}
int x = 5;
inc(x);
cout << x << endl; // prints 5
```
pass by value
```c++
void inc(int *n) {*n = *n + 1;}
int x = 5;
inc(&x);
cout << x << endl; // prints 6
```

```c++
cin >> n
operator>>(cin, n)    vs    scanf("%d", &x)
               not
          sending address of n
```
__Passed by Reference__

## References
```c++
int y = 10;
int &z = y;
```
z is a lvalue reference to y

- A reference is like a __constant pointer__ with automatic deferencing.
  
         -----                          -----                       -----
         | z |  --------------------->  | y | = (10) 12  <--------- | p |
         -----  cannot change this      -----                       -----
         z = 12; // automatic deferencing
         *z = 12; [X]
         int *p = &z; // give the address of y

  A reference has no identity of its own
  
  z is an alias of y (z is another name for y)
  
- cannot leave reference uninitialized
  
- cannot initialize a reference to something that is a a lvalue
  
        ------     -------
        |    |  =  |     |
        ------     -------
        lvalue      rvalue

- lavlue is a storage location, something that has an address

- `int &x = 5`; [X]

  `int &y = z + z;` [X]
  
- Cannot create a pointers to a reference
  `int &*y = ....;`[X]
  
- Cannot create a reference to a reference

- Cannot create an array of references

## Use of References
 1. References can be used as function parameters
 
 ```c++
 void inc(int &n) {n = n + 1;}
 int x = 5;
 inc(x);
 cout << x << endl; // print 6
 ```
 ```c++
 operator>>(cin, x);
 
 std::istream &operator>>(std::istream &in, int &data);
 ```
 using references everywhere: Streams cannot be copied

 2. Example:
  ```c++
  struct ReallyBig{ ... };
  int f(ReallyBig b) { ... };
  
  ReallyBig db = ....;
  f(db); // causes db to be copied (cost is big)
          // In C, we could prevent this by passing a pointers
  ```
  In C++, can also passed by reference
  ```c++
  int g(ReallyBig &rb) { ... };
  ```
   - prevent the need to copy into g's stack frame
  
   - any changes to rb are visible outside
  
 3. To disallow changes: pass by reference to const
  ```c++
  int h(const ReallyBig &rb) { ... }
  ```
  - cannot use rb to change the thing we are referencing
  
    __(Const apply to the thing on the left, usless there is nothing on the left then it applys to the things on the right.)__

 4. Exception
  ```c++
  void f(int &x) {...}
  void g(const int &y){...}
  
  f(5); X
  f(y+y); X
  
  g(5); V
  g(y+y); V \\ these two are allowed because it is promised that we won't change the value itself.
  
  int z = y + y;
  f(z); V
  ```
  
## Dynamic Memory
- In C,
 ```c
 int *p = malloc(num * sizeof(int));
 
  ...
 
 free(p);
 ```
 __Do Not use malloc/free/realloc__
 
 - malloc is prone to errors
 
- In C++, use new and delete
 ```c++
 struct Node{
   int data;
   Node *next;
 };
 
 Node *np = new Node;
  stack       heap
  
  ...
  
 delete np;
 ```
 __Note__:You should only give to delete a pointer that was returned by a previous call to new
 
 ```c++
 {
    Node n;
    Nde *np = new Node;
 }
 ```
 - stack allocated variables are deallocated
 
 - The heap Node has leaked
 
## Allocating arrays
  ```c++
  Node *npa = new Node[10];
  
  delete [] npa;
  ```
  
## Return by Value
  ```c++
  Node getMeANode() {
    Node n;
    return n; // create a copy to return
  }
  
  Node *getMeANode() {
    Node n;
    return &n;
  }
  ```
  The second one is dangerous because it may cause __Dangling Pointer__
  
  - pointing to memory that is no longer yours to use
  
  __Never return a pointer or reference to stack allocated data__
  
  ```c++
  Node *getNode() {
    Node *np = new Node;
    return np;
  }
  ```

























