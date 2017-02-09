## Lecture 12 ##

Last time

      a. Distructors
      b. Copy assignment operators


```
 Node n2 = plusOne(n); (temporary)
 tmp = ........
 Node n2 = tmp;//2 copy constructros calls
```

In c++11, rvalue references can be used to indicate temporary objects (Node &&)

###Move Constructor###

       classes / rvalue / nodemove.cc (in interminal)
       
       struct Node{
             Node(Node &&others)
             : data{others.data}, next{others.next}{
                 others.next = nullptr;
               }
          };
          
### Move Assignment Operator ###
 
         Node m;
         m = plusOne(n);// call operators, call copy constructor, plusOne(n) is rvalue
       
         Since rhs is a temp, let's steal
         
         struct Node{
              Node &Operator = (Node &&others){
                  swap(others);
                  return *this;
               }
            }
           
           
 If a move constructor/move assignment operators are implemented, these are called when the RHS is a rvalue\
 
 ### Copy / Move Elision ###
 
 ``` 
Vec makeAvec() {return {0,0};} (basic constructor)
 
  Vec v = makeAVec(); // either copy constructor or move constructor
  
  When you run this, only basic constructor runs;
  
  the values {0,0} get written directly into variable
  
  void doSomething(Vec v){
        .
        .
        .
        .
        .
  }
  
  doSomething(makeAVec());         (only basic constructor runs)
```

**In certain situations, c++ allows compilers to skip copy/move constructors, even if they have side effects**

**We are expected to know that it is possible, not exactly when it will occur**

To close this option, we can use "-fno-elide-constructors" to compiler

##Rule of 5##

  If you need to write a custom version of
  
     - copy constructor
     - distructor                             correctness
     - copy assignment operators
     
     - move constructor
     - move assignment operator               efficiency
     
     then you usually have to write all 5
     

**Note: Assignment operators must be implemented as a method**
Previously, we implemented + or * for Vec as functions

When you implement an operator as a method

```
Vec v{1,2};
Vec v{3,4};
Vec v2 = v + v1*k;

Struct vec{
       int x,y;
       }
       vector operators+(const vec &others){
              return {x + others.x, y+others.y};
           }
           Vec operators*(const int k){
               return {x*k, y*k};
           }
     };
     
Vec operators*(const int k, const vec &others){
         return v*k;
       }
       
Input / Output Operators as methods

Struct vec{
       ostream &operators<<(ostream &out)
               out << x << " " << y;
               return out;
           }
       };
       
 Vec v; 
 v << cout;        v.operator<<(cout);
 v1 << (v << cout) disgusting
```

In C++, following operators must be implemented as methors

      operators =
      operators []
      operators ->
      operators ()
      operators T()    ---- akkiws unokucut cibcersuib from Class to type T
      
      
**Arrays of Objects**

```
    Struct Vec{
           int x,y;
           Vec(int x, int y) : x{x}, y{y}{}
         };
     
    Vec vectors[3]   X won't compile
    Vec *vecs - new Vec[3] X won't compile
    
Trying to default construct elements of array

Optionss

1. provide default (0 parameter) constructor
2. for stack allocated arrays
        Vec vectors[3] = {Vec{0,1}, Vec{1,2}, Vec{3,4}};
3. for stack/heap arrays
        create arrays of Vec pointers
        
Vec *vp[10] // stack allocated array for 10 Vec pointers

Vec ** arr = new Vec *[10];
arr[0] = new Vec{1,2};
       .
       .
       .
       .
for (int i=0; int i<10; i++) delete arr[i];
delete [] arr;
```

Seperate Compilation with Classes
 
   .h ____ type defs of function headers
   
   .cc ____ implementation
   
 Place only the method headers in the header file
 ```
 
 classes/seperate/node.h
                 /node.cc
                 
  Node.h
        #ifndef NODE_H
        #define NODE_H
        struct Node{
              int data;
              Node *next;
              Node (int data, Node *next);
              Node (const Node &others);
        }
        #endif
        
   Node.cc
      Node::#include "node.h
         
         Node(int data, Node *next)
               :data{data}, next{next}{}
               
      :: scope resolution operators
      
      In the scope of class Node, there is a method called Node
```

Const Methods
```
Struct Student {
       int assns, mt, final;
       float grade() const
       {
         return assns*0.4 + mt*0.2 + final*0.4;
         }
       };
       
const Studnet billy{70,70,70};

billy.grade(); (won't compile because grade doesn't promise that it won't change any fields.

In C++, a method can process int to change any field by declaring the method const

billy.grade() works after adding const next to float grade();

compiler does check that you don't change field values
 
  
       
       


              

