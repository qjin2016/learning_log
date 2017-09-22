---
layout: post
title:  "Learning Log 1"
date:   2017-09-21 
categories: C++ Python OOP
image:  /preview.jpg
---
#### Learn C++ OOP, https://www3.ntu.edu.sg/home/ehchua/programming/cpp/cp3_OOP.html
- Private section is for static variable/data structure
- Public section is for functions
- Dot operator
- Constructor, a special function that has the function name same as the class name, used to construct and initialize all the data members
- Convention for getter/setter and constructors:

```c++
class Aaa
{
private:
  T xxx;

public:
  Aaa(T x) { xxx = x; }
  //OR
  Aaa(T xxx) { this -> xxx = xxx; }
  //OR
  Aaa(T xxx) : xxx(xxx) {}
  
  T getXxx() const { return xxx;}
  
  void setXxx(T x) { xxx = x;}
  //OR
  void setXxx(T xxx) { this -> xxx = xxx; }
}

```

