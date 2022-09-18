Disclaimer:
> **The shallow and deep copy makes sense only for compound objects (objects that contain other objects, like lists, sets, dictionaries, or class instances).**

In Python, when we use = operator to do something like this, `a = 4; b = a` we may think that this creates a new object; it doesn't. It only binds a new name to `4` that shares the reference of the original object (`4`). To give an example,


```python
old_list = [[1, 2, 3], [4, 5, 6], [7, 8, 'a']]
new_list = old_list

new_list[2][2] = 9

print('Old List:', old_list)
print('ID of Old List:', id(old_list))

print('New List:', new_list)
print('ID of New List:', id(new_list))
```

    Old List: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    ID of Old List: 2747833076096
    New List: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    ID of New List: 2747833076096
    

We see that both of the list object are same and share the same memory. So, if you want to modify any values in `new_list` or `old_list`, the change is visible in both.

Essentially, sometimes you may want to have the original values unchanged and only modify the new values or vice versa. In Python, there are two ways to create copies:

- Shallow Copy
- Deep copy

We need the `copy` to make this work.

## Shallow Copy

A shallow copy creates a new object (i.e. create a copy) which stores the reference of the original elements. Again This makes more sense for compound objects (container like objects, Set, list, dict etc).

So, a shallow copy doesn't create a copy of nested objects, instead it just copies the reference of nested objects. This means, a copy process does not recurse or create copies of nested objects itself.


```python
import copy

old_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
new_list = copy.copy(old_list)

print('Old List:', old_list)
print('ID of Old List:', id(old_list))

print('New List:', new_list)
print('ID of New List:', id(new_list))

old_list.append([4, 4, 4])

print("--"*40)
print("Old list:", old_list)
print("New list:", new_list)
```

    Old List: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    ID of Old List: 2747832824768
    New List: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    ID of New List: 2747833076864
    --------------------------------------------------------------------------------
    Old list: [[1, 2, 3], [4, 5, 6], [7, 8, 9], [4, 4, 4]]
    New list: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    

So its pretty much clear that `old_list` and `new_list` are different object now and adding nested objects at the most outer level to either list object doesn't change other.

But what happens if we change/modify the the nested objects?

That change will prevail in both of the object (original and copied), that's because copied object didn't copy the nested objects too, it only store the references of those nested objects.


```python
import copy

old_list = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
new_list = copy.copy(old_list)

old_list[1][1] = 'AA'

print("Old list:", old_list)
print("New list:", new_list)
```

    Old list: [[1, 1, 1], [2, 'AA', 2], [3, 3, 3]]
    New list: [[1, 1, 1], [2, 'AA', 2], [3, 3, 3]]
    


```python
import copy

old_list = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
new_list = copy.copy(old_list)

new_list[1][1] = 'AA'

print("Old list:", old_list)
print("New list:", new_list)
```

    Old list: [[1, 1, 1], [2, 'AA', 2], [3, 3, 3]]
    New list: [[1, 1, 1], [2, 'AA', 2], [3, 3, 3]]
    

Here both `new_list` and `old_list` share the same references to those nested objects.

## Deep Copy

A deep copy creates a new object and recursively adds the copies of nested objects present in the original elements. That is, deep copy creates a completely new object from outer most level to inner most.


```python
import copy

old_list = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
new_list = copy.deepcopy(old_list)

print("Old list:", old_list)
print("New list:", new_list)

old_list[1][0] = 'BB'

print("--"*40)
print("Old list:", old_list)
print("New list:", new_list)
```

    Old list: [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
    New list: [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
    --------------------------------------------------------------------------------
    Old list: [[1, 1, 1], ['BB', 2, 2], [3, 3, 3]]
    New list: [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
    

In the above program, when we assign a new value to `old_list`, we can see only the `old_list` is modified. This means, both the `old_list` and the `new_list` are independent. This is because the `old_list` was recursively copied, which is true for all its nested objects.

## More

There are some more ways to create a shallow copy other than using copy module.


```python
## using a loop

my_list1 = [10,20,30,40,50]
my_list2 = []

for num in my_list1:
    my_list2.append(num)

print(id(my_list1), id(my_list2))
```

    2747833076096 2747832749632
    


```python
## using list comprehension

my_list1 = [10,20,30,40,50]
my_list2 = [x for x in my_list1]

print(id(my_list1), id(my_list2))
```

    2747833073728 2747832816128
    


```python
## using copy method

my_list1 = [10,20,30,40,50]
my_list2 = my_list1.copy()

print(id(my_list1), id(my_list2))
```

    2747833076096 2747833068032
    


```python
## Slicing method
my_list1 = [10,20,30,40,50]
my_list2 = my_list1[:]

print(id(my_list1), id(my_list2))
```

    2747832816128 2747832155840
    


```python
## using constructor

my_list1 = [10,20,30,40,50]
my_list2 = list(my_list1)

print(id(my_list1), id(my_list2))
```

    2747833076864 2747832152256
    


```python

```
