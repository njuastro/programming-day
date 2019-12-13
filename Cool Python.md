
# Cool Python


```python
# The pythonic start
import this
```

# Lambda, map and reduce

The 'lambda function' is quickest way to define a one-time used function


```python
# Comparing lambda function with normal function

def square(x):
    return x * x

square_lambda = lambda x: x * x

assert square(3) == square_lambda(3)
print(' square: {}\n square_lambda: {}'.format(square(3), square_lambda(3)))
```

`map` can be used to apply a function to all the elements in a list or array.


```python
# map
nums = [1, 2, 3, 4, 5]
nums_squared = map(square, nums)
nums_squared_lambda = map(lambda x: x * x, nums)

print(list(nums_squared))
print(list(nums_squared_lambda))
```


```python
# change all the integers into str
list(map(str, nums))

# change all the integers into float
list(map(float, nums))
```

The `reduce(fun, seq)` function is used to apply a particular function passed in its argument to all of the list elements mentioned in the sequence passed along. Unlike the `map`, this function is defined seperately in “functools” module.


```python
# reduce
from functools import reduce

# computing 5!
nums = [1, 2, 3, 4, 5]
product = reduce(lambda x, y: x * y, nums)
print(product)
```

# List

The most commonly used data type in python, you can use the `append` and `pop` method to add new element and remove the last element from the list. To remove a specific element, using the `del` command.


```python
weekdays = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']

weekdays.append('Sat')
print(weekdays)
weekdays.pop()
print(weekdays)
```

    ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']
    ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']



```python
# a fancy way to insert numbers
nums = [1, 2, 3, 4, 5]

nums[1:1] = [0.2, 0.3, 0.5]
print(nums)
```




One line to construct a list:


```python
[x if x%2 else x*100 for x in range(1, 10)]
```



## 1. Index and slicing

Python list support negative index and also the magic slicing syntax: $[star:end:step]$. 


```python
# define the list
nums = [1, 2, 3, 4, 5]
```


```python
# the last element of the list
nums[-1]
```


```python
# reverse the whole list
nums[::-1]
```


```python
# select every other number
nums[::2]
```


```python
# select every other number and reverse the order
nums[-2::-2]
```

## 3. Unpacking and swapping

Unpacking a list by each element like this:


```python
a = [1, 2, 3]
x, y, z = a
print(x, y, z)
```

A more advanced unpacking can be find in the following [section](#The-usage-of-%22_%22). Also, swapping two elements is super easy:


```python
print(x, y)
x, y = y, x
print(x, y)
```

## 4. Flattening

There are several ways to unpack a list, for a list of lists:


```python
list_of_lists = [[1], [2, 3], [4, 5, 6]]
sum(list_of_lists, [])
```

To flatten a nested list, you may need the lambda function to flatten it recursively.


```python
nested_list = [[1, 2], [[3, 4], [5, 6], [[7, 8], [9, 10], [[11, [12, 13]]]]]]
flatten = lambda x: [y for l in x for y in flatten(l)] if type(x) is list else [x]
flatten(nested_list)
```

Another tool to flatten a list is the `itertools`, which is newly introduced by Python3.


```python
import itertools
a = [[1], [2, 3], [4, 5, 6]] 
print(list(itertools.chain.from_iterable(a)))
```

    [1, 2, 3, 4, 5, 6]
    [1, 2, [3, 4], [5, 6], [[7, 8], [9, 10], [[11, [12, 13]]]]]


## 5. enumerate and zip

`enumerate` makes it easier to get the index and value of a list at the same time.


```python
weekdays = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']
for i,j in enumerate(weekdays):
    print(i, j)
```

    0 Mon
    1 Tue
    2 Wed
    3 Thu
    4 Fri


An alternative ways is the `zip` function, which is to map the similar index of multiple containers so that they can be used just using as single entity. 


```python
nums = [0, 1, 2, 3, 4]
weekdays = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']
list(zip(nums, weekdays))
for i,j in zip(nums, weekdays):
    print(i, j)
```

    0 Mon
    1 Tue
    2 Wed
    3 Thu
    4 Fri


# iterator

Iterator in Python is any Python type that can be used with a ‘for in loop’. In Python3, an iterator is the object which consist `__iter__()` and `__next__()` methods


```python
class TestIterator: 
    # Cosntructor 
    def __init__(self, limit): 
        self.limit = limit 
    # Called when iteration is initialized 
    def __iter__(self): 
        self.x = 10
        return self
    # To move to next element
    def __next__(self): 
        # Store current value ofx 
        x = self.x 
        # Stop iteration if limit is reached 
        if x > self.limit: 
            raise StopIteration 
        # Else increment and return old value 
        self.x = x + 1; 
        return x 
    
for i in TestIterator(15): 
    print(i) 
```


```python
# The difference between list and iterator
new_list = [1, 2, 3, 4]
new_iterator = iter([1, 2, 3, 4])
new_iterator
```


```python
for item in new_list:
    print(item)
```


```python
for item in new_iterator:
    print(item)
```

Actually, all the Python internal type like list, tuple, dict and sets are all iterators. The commonly used functions `zip` and `map` return iterator by default, that is different from Python2. To print all the elements in `zip` and `map`, you need to convert them into list or print all the elements in a loop. 


```python
# different from python2
nums = [0, 1, 2, 3, 4]
weekdays = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']
print(list(zip(nums, weekdays)))
print(list(map(lambda x: x * x, nums)))
```


```python
import itertools as it

print(list(it.combinations([1, 2, 3], 2)))
print(list(it.permutations(['a', 'b', 'c'])))
print(list(it.repeat(2, 5)))
```

# The usage of "_"

1. Refer to the last executed expression


```python
a = 20
a
```


```python
_
```

2. Ignoring the values


```python
x, _, y = (1, 2, 3)
print(x, y)
```


```python
x, *_, y = (1, 2, 3, 4, 5)
print(x, y)
```


```python
for _ in range(3):
    # do something for 10 times
    print('Coffee break is great!')
```

3. convention could be used for avoiding conflict with Python keywords (convention), like the 'class_' or 'list_' you can define.

4. separating digits of numbers using *underscore* for readability


```python
a = 1_000_000
a
```

5. Magic method


```python
class A:
    def __init__(self, a, b):
        self.a = a
        self.__b = b
    def __len__(self):
        return 2
    def __str__(self):
        pass
    def __mangling(self):
        pass

print(A.__dict__)

a = A(1, 2)
print(a.__dict__)
```




For variable started with two underlines, it follows python “mangling” rules which adds the “_ClassName” to front of attribute names. It is used to avoid accidental overloading of methods and name conflicts with superclasses' attributes. It can be quite useful if you write a class that is expected to be extended many times. See [this](https://stackoverflow.com/questions/7456807/python-name-mangling) for detail.

6. Private naming


```python
_internal_name = 'private_name' # private variable
_internal_version = '1.0' # private variable
class _Base: # private class
    _hidden_factor = 2 # private variable    
    def __init__(self, price):
        self._price = price    
    def _double_price(self): # private method
        return self._price * self._hidden_factor    
    def get_double_price(self):
        return self._double_price() 
```

Alternative way to prevent users import all the class:


```python
 __all__ = ['Class1', 'Class2']
    
class Class1:
    pass
class Class2:
    pass
class Class3:
    pass
```

# Formatting a string

1. C-style string formatting


```python
name = "John"
age = 23
print("%s is %d years old." % (name, age))
```

'%s' can be used to covert any object to a string


```python
mylist = [1,2,3]
print("A list: %s" % mylist)
```

2. format (Python3+)


```python
name = "John"
age = 23
print("{} is {} years old.".format(name, age))
print()
```

3. The f-string expression (Python 3.6+)


```python
name = 'world'
print(f"hello {name}")
```

4. Template string (standard library)


```python
from string import Template
t = Template('Hey, $name!')
t.substitute(name=name)
```

# The end

If you think python is so great, please do not forget to check [What's the f*ck Python](https://github.com/satwikkansal/wtfpython)

Also, another surprise:


```python
import antigravity
```

Reference:

1. [Chip Huyen: Python is cool](https://github.com/chiphuyen/python-is-cool)
2. [Hackernoon: What makes the Python Cool.](https://hackernoon.com/what-makes-the-python-cool-426e4c576685)
3. [Hackernoon: Understanding the underscore( _ ) of Python](https://hackernoon.com/understanding-the-underscore-of-python-309d1a029edc)

3. [GeekforGeeks: 10 Interesting Python Cool Tricks](https://www.geeksforgeeks.org/10-interesting-python-cool-tricks/)

4. [RealPython: itertools in python3, By example](https://realpython.com/python-itertools/)

5. [RealPython: Python String Formatting Best Practices](https://realpython.com/python-string-formatting/)



Find python package:

1. [Awesome-python](https://github.com/vinta/awesome-python)

Python Coding guide

[Google: Python Coding Style](https://google.github.io/styleguide/pyguide.html)


