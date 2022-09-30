## Object Introspection


```python
b = [1, 2, 3]
```


```python
b?
```


```python
def add_numbers(a, b):
    """
    Add two numbers
    
    Returns
    --------
    the_sum: type of arguments
    """
    return a + b
```


```python
add_numbers?
```


```python
a = [1, 2, 3]

b = a

b
```




    [1, 2, 3]




```python
a.append(4)
```


```python
b
```




    [1, 2, 3, 4]



**So we can see that, here both a and b is just a reference to the object `[1, 2, 3]`**

## Pass by value and Pass by reference

[See this](python-passing.md)

## Deep copy and Shallow copy in python

[See this](Deep-copy-and-Shallow-copy.md)

## Checking the Type



```python
a = 5; b = 4.5

isinstance(a, int)
```




    True




```python
isinstance(a, (int, float))
```




    True




```python
isinstance(b, (int, float))
```




    True



## Accessing Attributes and methods


```python
a = "foo"

getattr(a, "split")
```




    <function str.split(sep=None, maxsplit=-1)>



`getattr`, `setattr`, `hasattr` are used effectively to write generic and reusable code.

## Duck Typing


Often without caring about the type of an object, focusing on whether that object has certain methods or attributes is known as Duck typing. That if it walks like a duck, quacks like a duck, then its a duck.


```python
iter(1)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In [47], line 1
    ----> 1 iter(1)
    

    TypeError: 'int' object is not iterable



```python
def isiterable(obj):
    try:
        iter(obj)
        return True
    except TypeError:
        return False
```


```python
isiterable("af")
```




    True




```python
isiterable([1, 2, 3])
```




    True




```python
isiterable(1)
```




    False



**A module is a file with the extension `.py`**


```python
a = 9
b = 2

a // b # interger division
```




    4




```python
a % b # reminder
```




    1



To check whether two variables refer to the same object, we can use keyword `is` and `is not`


```python
a = [1, 2, 3]

b = a

c = list(a)
```


```python
a is b
```




    True




```python
c is a
```




    False




```python
print(f"id of a: {id(a)}")
print(f"id of b: {id(b)}")
print(f"id of c: {id(c)}")
```

    id of a: 1255757929600
    id of b: 1255757929600
    id of c: 1255751927872
    

**`list()` always creates a new python list (i.e. a copy)**


```python
a = None

type(a)
```




    NoneType




```python
a is None
```




    True




```python
a == None
```




    True




```python
None == None
```




    True




```python
None is None
```




    True



## Mutable and Immutable objects

**`list`, `dict`, Numpy arrays, user defined classes are mutable**

**strings, tuple are immutable.**

Standard python scaler types are

- `None` (only one instance of the `None` object exists.
- `str`
- `bytes` (raw binary data)
- `float`
- `bool`
- `int`


```python
c = """
This is a longer string that spans multiple 
times.
"""
```

Here c contains four lines of text, due to line breaks after `"""` and after the lines


```python
c.count("\n")
```




    3



If we want to modify the string, we need to use such function that creates new string and perform what need to be done on the new string.

Strings are unicode characters, so can be treated like other sequences in python.

If we need to interpret a string with lots of special character like back-slashes as is, we may use the raw string, `r"..."`.


```python
s = r"this\has\no\special\chars"
s
```




    'this\\has\\no\\special\\chars'




```python
"{0:.2f} {1:s} are worth US${2:d}".format(88.46, "Argentine Pesos", 1)
```




    '88.46 Argentine Pesos are worth US$1'




```python
f"{88.46:.2f} Argentine Pesos are worth US${1:d}"
```




    '88.46 Argentine Pesos are worth US$1'



## Bytes and Unicode


```python
val = "español"

utf_8 = val.encode("utf-8")

utf_8
```




    b'espa\xc3\xb1ol'




```python
type(utf_8)
```




    bytes




```python
utf_8.decode("utf_8")
```




    'español'




```python
val.encode("latin1")
```




    b'espa\xf1ol'




```python
val.encode("utf-16")
```




    b'\xff\xfee\x00s\x00p\x00a\x00\xf1\x00o\x00l\x00'



`encode` translates the string to its encoding specfic bytes representation and `decode` translate the bytes back to string assuming we know the encoding.

## Date and Times


```python
from datetime import datetime, date, time

dt = datetime(2011, 10, 29, 20, 30, 21)

dt
```




    datetime.datetime(2011, 10, 29, 20, 30, 21)




```python
dt.strftime("%Y-%b-%d %H:%M")
```




    '2011-Oct-29 20:30'




```python
datetime.strptime("20091031", "%Y%m%d")
```




    datetime.datetime(2009, 10, 31, 0, 0)



`strftime` is a method for datetime object that can be used to format datatime object and `strptime` is a function from `datetime` module that parse a string into datetime.

**datetime.datetime** is an immutable type.


```python
dt2 = datetime(2011, 11, 15, 22, 30)
```


```python
delta = dt2 - dt

delta
```




    datetime.timedelta(days=17, seconds=7179)



So difference of 17 days and 7179 secs


```python
dt + delta
```




    datetime.datetime(2011, 11, 15, 22, 30)




```python
sqnc = [1, 2, None, 4, None, 5]

without_none = [val for val in sqnc if val is not None]

without_none
```




    [1, 2, 4, 5]




```python
sequence = [1, 2, 0, 4, 6, 5, 2, 1]

without_5 = [val for val in sequence if val != 5]

without_5
```




    [1, 2, 0, 4, 6, 2, 1]



`break` only breaks the inner most loop, any outer loop will continue to run
