# Lecture 9
## Last time
  - Preprocessor
  - Separate Compilation
  
    ```c++
    g++14 -c vector.cc   => just compile
    g++14 -c main.cc     => creates object file(.o extension)
    g++14 main.o vector.o -o program
    ```
  - Never compile a `.h` file
  
    Never include a `.cc` file
    
----------------------

## Global Variable

In header file, declare but don't define the global.

- Example 1
  ```c++
  In abc.h

  extern int global;

  In abc.cc

  int global;
  ```

- Use preprocessor to prevent including headers file multiple times.
  
  __Inlucde Guards__
  
  "vector.h"
  
  ```c++
  #ifndef VECTOR_H
  #define VECTOR_H
  
  struct Vec{
    ...
    ...
  };
  
  #endif  
  ```
 - __Always include an include guard.__
 
 - Never use "using namespace std;" in hearder files
 
 - Always refer to things in std using std::cout, std::cin and so on.
 
## Classes

   Big innovation in Object Oriented Programming
   
   __"You can pu functions inside a struct"__
   
 - Example
  ```c++
  struct Student{
    int assns, mt, final;
    float computeGrade() {
      return 0.4 * assns + 0.2 * mt + 0.4 * final;
    }
  };
  
  Student billy{80,70,60};
  cout << billy.computeGrade() << endl;
  ```
  ```c++
  cin.clear()
  cin.ignore()
  str.length()
  ```
 - A __Class__ is a struct type that can potentially contain functions.
 
 - An instance of a class is called an object.
 
   (billy is an object of class Student)
   
 - A function defined inside a class is called a member function or a method.
 
   (computeGrade is a method)
   
 - A method can only be called on objects of the class.
 
   Inside the method, the method has access to the fields of the object on which the method was called.
  
 - Function vs Method
  - A method has access to a special hidden parameter called "this".
  - "this" is a pointer to the objecton which the method was called.
    ```c++
    billy.computeGlobal()
    inside the method
      this == &billy
    ```
    
    or
    
    ```c++
    struct Student {
      int assns, mt, final;
      float computeGrade() {
        return 0.4 * this->assns + 0.2 * this->int + 0.4 * this->final;
      }
    }
    ```
    
## Initializing Objects
   ```c++
   Student billy{80, 70, 60};  -> compile time constants
   ```
  - In C++, you can construct objects by calling a method called __constructor__
   
   ```c++
   struct Student {
      ...
      ...
      Student(int assns, int mt, int final) {   // name is same as class, no return type
        this->assns = assns;
        this->mt = mt;
        this->final = final;
      }
   };
   ```
  - Very common to name parameters of ctors the same as fields.
   
   `Student billy{60,70,80};` and 
   
   `Student billy = Student{60,70,80};` works exactly the same.
   
  - Note on uniform initialization
    ```c++
    int x = 5;
    string s = "hello";
    ```
    
    all equal to
    
    ```c++
    int x(5);
    string s("hello");
    Student billy(60,70,80);
    ```
  
  - Since C++11, the recommended way is to use "uniform initialization", using `{}`
  
  - Synamic Memory
    ```c++
    Student *pBilly = new Student{60,70,80};
    ```
 
 - Advantages of ctors
  - Function overloading, class invariant checks(sanity check)
    ```c++
    struct Student{
      ...
      ...
      Student(int assns=0, int mt=0, int fianl=0) {
        this->assns = assns;
        this->mt = mt;
        this->final = final < 0 ? 0 : final;
      }
    };
    
    Student xyz{70,60};  // final = 0;
    Student abc{};
    Student abc;
    ```
    
- Every class comes with a default constructor(0 parameters)
 
  calls default ctors on all field that are objects.
   
  
  
  
  
  
  
  
  
  
  
