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

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
