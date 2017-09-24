---
layout: post
title:  "Learning Log 3"
date:   2017-09-23 
categories: Python OOP
image:  /preview.jpg
---
#### OOP in Python (https://www.youtube.com/watch?v=rq8cL2XMM5M&list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc&index=3)
*class variable vs. instance variable
```python
class Employee:
  # class variable
  num_of_emps = 0
  
  def __init__(self):
    Employee.num_of_emps += 1
```
*self is used to refer to instance

*class methods vs instance methods

  * class method is an alternative way for constructor
  
```python
class Employee:
  # class variable
  raise_amt = 1.04
  
  def __init__(self, first, last, pay):
    self.first = first
    self.last = last
    self.pay = pay
    Employee.num_of_emps += 1
    
  @classmethod
  def set_raise_amt(cls, amount):
    cls.raise_amt = amount
    
  @classmethod
  def from_string(cls, emp_str):
    first, last, pay = emp_str.split('-)
    # alternative constructor
    return cls(first, last, pay)
    
emp_str_1 = 'John-Doe-7000'
new_emp_1 = Employee.from_string(emp_str_1)
```





