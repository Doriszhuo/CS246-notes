# Lec 13

## const method
```c++
struct Student{
  int assns, mt, final;
  float grade() const {
    return assns * 0.4 +
           mt * 0.2 +
           final * 0.4;
  }
};

const Student billy{70,70,70};
billy.grade();
```
