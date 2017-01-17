# Lec 5: C++ I/O

## Last time:

1. Hello world 
 ```c++
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

-----------

- When you `include <iostream>`, you get access to 3 global variables(streams)
  - cout: connected to standard output
  - cin: connected to standard input
  - cerr: connected to standard error
  
- Two I/O operators
  - `<<`: output operator
    
    ex: `cout << "Hello"`, `cerr<< "Bad!"`
    
  - `<<`: input operator
  
    ex: `cin >> xyz`
    
- __Example__: Add two numbers
 ```c++
 #include <iostream>
 using namespace std;
 int main() {
    int x, y
    cin >> x >> y;
    cout << x + y << endl;
 }
```
  __NOTE__: `cin` will continue to wait for input
    - it ignores whitespace
    - if a read fails (e.g. non int provided when trying to read an in, EOF), the program seems to continue
    - important to check whether the read succeed
  
  __HOW to CHECK__
    - If a read fails, the expression `cin.fail()` is true
    - If a read fails due to EOF, the expressions `cin.fail()` and `cin.eof()` are true
  
- __Example 2__:

  Read all ints from stdin and echo them one per line. Stop if a read fails
 	```c++
  #include <iostream>
  using namespace std;
  int main() {
    int x;
    while (true) {
      cin >> x;
      if(cin.fail()) break;
      cout << x << endl;
    }
  }
  ```
  There are an automatic/implicit conversion from cin(type:istream) to boolean
  
  cin is true if cin.fail() is false
  
  Thus, we can write like this:
  ```c++
  #include <iostream>
  using namespace std;
  int main() {
    int x;
    while (true) {
      cin >> x;
      if(!cin) break;  -> if cin.fail() is true, cin is false
      cout << x << endl;
    }
  }
  ```
  __Note__: 
   - `cin >> x` provides the value of `cin`. This is why we can write `cin >> x >> y >> z` (after reading into x, it becomes `cin >> y >> z` and keep going)
   - If a read fails, all subsequent reads fail
   
  __Note2__: in C, `>>` is bit shifting operator (operator overloading)
  
  ```c++
  #include <iostream>
  using namespace std;
  int main() {
    int x;
    while (true) {
      if (!cin >> x) break;
      cout << x << endl;
    }
  }
  ```
  alternative(the cleanest type):
  ```c++
  #include <iostream>
  using namespace std;
  int main() {
    int x;
    while (cin >> x) {
      cout << x << endl;
    }
  }
  ```
- __Example 3__:

  Read and echo all ints, ifnore non-ints. Stop at EOF
  ```c++
  int main() {
    int i;
    while(true) {
      if(cin >> i) {
        cout << i << endl;
      } else {
        if(cin.eof()) break;
        else { // read bad input
          cin.clear(); // clear the flag
          cin.ignore(); // ignore the input causing fails and move on
        }
      } // end else
    } // end while
  } // end main
  ```
- __Example 4__:
  
  Read a string:
  ```c++
  #include <iostream>
  #include <string>
  using namespace std;
  
  int main() {
    string s;
    cin >> s;
    cout << s << endl;
  }
  ```
  What is I want to read the entire line?
  ```c++
  #include <iostream>
  #include <string>
  using namespace std;
  
  int main() {
    string str;
    getline(cin, str);
    cout << str << endl;
  }
  ```

- Formal Specification
  ```c++
  int x = 95;
  cout << x; // prints 95 in decimals
  ```
  What is I want to print in hexadecimals: __Use I/O Manipulator__
  ```c++
  #include <iomanip>
  
  int x = 95;
  cout << hex << x;  -> dose not produce ouput, changes cout to print int values in hex
  cout << dec; -> change back to decimals
  ```

- (Not) Skipping whitespace: see `<iomanip>`

- Reading/Writing to files
  ```c++
  #include <fstream>     --> ifstream: input file stream
                         --> ofstream: output file stream
  int main() {
    ifstream f{"file.txt"};
    while (f >> s) {
      cout << s << endl;
    }
  }
  ```
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
