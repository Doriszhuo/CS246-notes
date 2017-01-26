# Lec 8

## Last time
  - References
  - Dynamic Memory
  
------------

## Operator Overloading
 - `<<`, `>>` are overloaded
 - `+`
 
 In C++, operators can be overloaded for user defined types.
 
 In C:
 ```c
 Struct Vec{
    int x;
    int y;
 };
 add(v1, v2); // ugly
 
 v1 + v2; // pretty
```

So let's overload  operator
```c++
Vec operator+(const Vec &v1, const Vec &v2) {
   Vec v{v1.x + v2.x, v1.y + v2.y};
   return v;
}
```
__Note:__ Pass by references: save the cost
 
```c++
Vec operator*(cosnt int k, const Vec &v1) {
  return {k * v1.x, k * v1.y};
}

3 * v; V
v * 3; X

Vec operator*(const Vec &v1, const int k) {
  return k * v1;
}

v * 3; X
```

- Output Operator <<

  ```c++
  struct Grade{
    int theGrade;
  };
  
  ostream &operator<<(ostream &out, const Grade &g) {
    out << g.theGrade << "%";
    return out;
  }
  
  Grade g;
  cout << g;
  ```
  
  __Note:__ Using reference to for stream return: stream doesn't allow copying.

- Input Operator >>
  
  ```
  istream &operator>>(istream &in, Grade &g) {
    in >> g.theGrade;
    if(g.theGrade > 100) g.theGrade = 100;
    if(g.theGrade < 0) g.theGrade = 0;
    return in;
  }
  
  cin >> g;
  ```
  
## Preporcessor
 - preprocessor runs before the compiler
 
 - changes code sent to the compiler
 
  `#include<iostream>` --> preprocessor directive
   - copies and paster the contents of iostream
 
 - `<----->` --> search standard include
    
    "____"____ // in current direction
    
 - preprocessor output
   ```c++
   g++14 -E dile
   ```
 - Define
   ```c++
   #define VAR VALUE
      preprocessor variable
   ```
   search and replace VAR for VALUE
 
 - Define constants
   ```c++
   #define MAX 10
     .
     .
     .
   int arr([MAX]);
   ```
   __Note:__ C/C++ have const, Don't use define for it anymore.
   
   
   
## Conditional Compilation

 BBOS____  long long int publickey;

 IOS____   short int pulickey;
 
 ```c++
 #if  ...
    ....      (nests)
    ....
 #endif
 ```
 
 ```c++
 //_____ single line comments
 
 --------------------------------
 
 /*
    /*
        /*  (block comment)
        
     */
 ```
 
## Debugging
 debug.cc
 ```c++
 #incldue <iostream>
 
 int main() {
  #ifdef DEBUG
    cout << "setting x = 1" << endl;
  #endif
  int x = 1;
  while(c<10) {
   ++x;
   #ifdef DEBUG
   cout << "x is now" << x << endl;
   #endif
  }
  cout << x << endl;
 }
 ```
 ```c++
 g++14 -DDEBUG debug.cc
 ./a.out
 
 g++14 debug.cc
 ./a.out
 ```
 
 Definings vars on the command line
 preprocess.cc
 ```c++
    g++ -E -DOS=IOS  preprocess.cc
           -DOS=BBOS
 ```
 ```c++
 #define VAR  --> value becomes empty string
 #ifdef VAR  - true if VAR is defined
 #ifndef VAR - true if VAR is not defined
 ```
 
## Separate Compilation
  Interface(.h)
  
    - type definitions
    
    - function headers
    
  Implementation(.cc)(`#include ".h"`)
  
    - implements functions
    
 __NOTE:__ Never ever compile a .h file
 
 __NOTE2:__ Never ever include a .cc file
 
 We want to compile separtely:
 ```c++
 g++ -c main.cc
 g++ -c vector.cc
 
 Creates object files:
    main.o vector.o
 
 Link them:
 g++14 main.o vector.o
 
 ./a.out
 ```
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
