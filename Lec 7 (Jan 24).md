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
z is a evalue reference to y

- A reference is like a __constant pointer__ with automatic deferencing.
  
         -----                          -----                         -----
         | z |  --------------------->  | y | = (10) 12  <--------- | p |
         -----  cannot change this      -----                         -----
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
- References can be used as function parameters
 
 ```c++
 void inc(int &n) {n = n + 1;}
 int x = 5;
 inc(x);
 cout << x << endl; // print 6
 ```








