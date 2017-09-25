---
layout: post
title:  "Learning Log 3"
date:   2017-09-23 
categories: Python OOP C++ LeetCode WiggleSort2
image:  /preview.jpg
---
#### OOP in Python (https://www.youtube.com/watch?v=rq8cL2XMM5M&list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc&index=3)
- class variable vs. instance variable
```python
class Employee:
  # class variable
  num_of_emps = 0
  
  def __init__(self):
    Employee.num_of_emps += 1
```
- self is used to refer to instance

- class methods vs instance methods

  - class method is an alternative way for constructor
  
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
- class method passes cls as the first argument, instance method passes self as the first argument, while static method doesn't pass cls or self. Static method doesn't operate on class or instance.

```python
class Employee:
  # class variable
  raise_amt = 1.04
  
  def __init__(self, first, last, pay):
    self.first = first
    self.last = last
    self.pay = pay
    Employee.num_of_emps += 1
    
  @staticmethod
  def is_workday(day):
    if day.weekday() == 5 or day.weekday() == 6:
      return False
    else:
      return True
    
import datetime
my_date = datetime.date(2017, 7, 10)
print(Employee.is_workday(my_date))
```

- subclasses, inheritance

```python
class Developer(Employee):
  pass
  
# get resolution
print(help(Developer))

class Developer(Employee):
  def __init__(self, first, last, pay, prog_lang):
    super().__init__(first, last, pay)
    # or
    # Employee.__init__(self, first, last, pay)
    
    self.prog_lang = prog_lang

dev_1 = Developer('xx', 'xx', xxx, 'Python)
print(isinstance(dev1, Developer))
print(issubclass(Developer, Employee))
```

- magic methods, used for printing object or customizing certain operations

```python
class Employee:
  # class variable
  raise_amt = 1.04
  
  def __init__(self, first, last, pay):
    self.first = first
    self.last = last
    self.pay = pay
    Employee.num_of_emps += 1
    
  # used for debugging purpose
  # print(emp) will get the same results as print(emp.__repr__()) 
  def __repr__(self):
    return "Employee('{}', '{}', {})".format(self.first, self.last, self.pay)
    
  # similar as __repr__
  def __str__(self):
    return "{} - {}".formate(self.fullname(), self.email
  
  # add two employees salary
  # use like this: emp1 + emp2
  def __add__(self, other):
    return self.pay + other.pay
```

- property decorators - getter, setter, deleter, to define a method and access it like an attribute

```python
class Employee:
  
  def __init__(self, first, last):
    self.first = first
    self.last = last
  
  @property 
  def email(self):
    return '{}.{}'.formate(self.first, self.last)
    
  @property
  def fullname(self):
    return '{} {}'.format(self.first, self.last)
    
  @fullname.setter
  def fullname(self, name):
    first, last = name.split(' ')
    self.first = first
    self.last = last
    
  @fullname.deleter
  def fullname(self, name):
    print('delete name!')
    self.first = None
    self.last = None
  
emp1 = Employee('Jone', 'Smith')
print(emp1.email)

emp1.fullname = 'Corey Sh'

del emp1.fullname
```

### Leetcode, Wiggle Sort (https://leetcode.com/problems/wiggle-sort-ii/description/)

### Leetcode 297, Serialize and Deserialize binary tree (https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)


