# Lecture 6
## Last time
  - C++ I/O
  - IO Manipulation
    `<fstream>`
    - ifstream
    - ofstream
   ```c++
   #include <fstream>
   int main() {
     ifstream f{"myfile.txt"}; // tells the OS to open the file
     string s;
     while (f >> s) {
       cout << s << endl;
     }
   }
   ```
   __Note__: File is closed when f goes out of scope.

------------------

- We can treat strings as data streams

 ```c++
 <sstream>
 ```
  - istringstream
  - ostringstream
  
  __Example__: 
  ```c++
  int low = ..., int high = ...
  ostringstream ss;
  ss << "Please input a value between" << low << "and" << high; //packed the whole string inside ss
  string s = ss.str(); // output the string
  ```

- Example: getNum.cc
  ```c++
  int n;
  while(true) {
    cout << "Enter Number" <<endl;
    string s;
    cin >> s; // use string, nothing make this fail until EOF
    istringstream ss{s}; // ss treats s as an input
    if (ss >> n) break; // this will succeed only if the stirng ss is a number
    cout << "That's not a number" << endl;
  }
  ```
  equals
  ```c++
  #include <iostream>
  #include <sstream>
  using namespace std;
  
  int main () {
    string s;
    while (cin >> s) {
      istringstream ss{s};
      int n;
      if (ss >> n) cout << n << endl;
    }
  }
  ```

- C++ string
  C uses `char *` to simulate strings
    - null terminated `\0`
    - explicit memory management
    - easy to mess up
  
  C++ string type does automatic memory management
    - `string s == "hello";`
      
      __Note__: `string s` C++ string; `"hello"` C style string
      
    - Comparison:
    
      |  | __C__ | __C++__ | 
      |-----|:----:|:----:|
      | __equality__ | stremp | s1 == s2 |
      | __<, >__ | // | <, > |
      | __concatenation__ | strcat(c1, c2) | s1 = s1 + s2 |
      | __length__ | strlen | s.length() |
      | __access chars__ | s[0], s[1], ... | s[0], s[1] | 
  
- Default Arguments in C++
  ```c++
  void printFile(string name = "myfile.txt"){
    string s;
    ifstream f{name};
    while (f >> s) {
      cout << s << endl;
    }
  }
  ```
  
  `printFile();` - print the default file
  
  `printFile("other.txt");` - print the file you choose
  
  __Big Rule__: You cannot follow a default argument with a non-default argument
  
  `void test(int num = 0, string str)` __WON'T WORK__
  
  has to be `void test(int num = 0, string str = "hello")`
  
  Then, 
  
  `test(5, "mystring");` --> test(int, string);
  
  `test(s);` --> test(int);
  
  `test();` --> test();
  
  `test(,"mystring");`  ->__not possible__
  
- Function Overloading
  - In C
    ```c
    int negint(int a) { return -a; }
    bool negbool(bool a) { return !a; }
    ```
    cannot name both these functions the same
  
  - C++
  
    allows naming function the same as long as the numbers of argument and/or types of args have a difference
    
  - Example:
  
    `cin >> i`; `>>`: input operator ==> `operator>>(cin,i)`
    
    `int x = 2; x >> 3`; `>>` right bit shift ==> `operator>>(x,5)`
    
- Struct
  - In C
    ```c
    struct Node{
      int data;
      struct Node *next;
    };
    struct Node n1 = {3,4};
    ```
    
  - C++
    ```c++
    struct Node{
      int data;
      Node *next; // cannot put "Node next" here, because the compiler cannot calculate size
    };
    Node n1 = {3,4};
    ```
    
- Constants
  - `const int max = 10;`
  - `const Node n1{5, nullptr};`
  
    `nullptr` is a new keyword in C++11, __DO NOT USE `NULL`__
    
  - .
    ```c++
    int n = 5;
    const int *p = &n; // p is a point pointing to a constant integer
    ```
    
    `p = &m;` [x]
    
    `*p = 3;` v
    
    `n = 3;` v
    
  - .
    ```c++
    cont int n = 5;
    int * const p = &n; // p is a constant pointer pointing at an integer
    ```
    ```c++
    p = &m; x
    *p = 3; v(will still work, but may cause problems)
    ```
  
    
  
  
  
  
  
  
  
  
  
  
