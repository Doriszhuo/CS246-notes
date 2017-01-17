# Lec 5: C++ I/O

## Last time:

1. Hello world 
 ```ruby
  #include<iostream>
  using namespace std;
  int main() {
     cout << "Hello world" << endl;
     return 0;
  }
 ```
 
2. Compling
 ```ruby
 g++-5 -std=c++14 file.cc -o prog
 ```
 default program name: `a.out`

-----

- When you include <iostream>, you get access to 3 global variables(streams)
  - cout: connected to standard output
  - cin: connected to standard input
  - cerr: connected to standard error
  
- Two I/O operators
  - `<<`: output operator
    
    ex: `cout << "Hello"`, `cerr<< "Bad!"`
