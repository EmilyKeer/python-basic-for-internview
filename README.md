### checklist
- list copy  append: 
	- l1 = l2: l1 is a pointer to l2
	- l1 = l2[:] copy the 1D array
- `//` devide
- when copy list: l1 = l2[:]
	- Copy a 2D matrix: `nextState = [x[:] for x in curState]`
- pow: `x**2` instead of `x^2`
- Change value and assign:

```
# This is not right:
dic = dict() #[1, dict()]
dic[k] = 1, dict()]
dic[k] = [num, dic[k][1]]

Should be:
tmp = dic[k][1]
dic[k] = [num, tmp]
```

### for loop for list
If you need to modify the sequence you are iterating over while inside the loop (for example to duplicate selected items), it is recommended that you first make a copy. Iterating over a sequence does not implicitly make a copy. The slice notation makes this especially convenient:

```
>>>
>>> for w in words[:]:  # Loop over a slice copy of the entire list.
...     if len(w) > 6:
...         words.insert(0, w)
...
>>> words
['defenestrate', 'cat', 'window', 'defenestrate']
```

```
>>> list(range(5))
[0, 1, 2, 3, 4]
```

```
if len(matrix[0]) == 1:
    return [col_val for row in matrix for col_val in row]

blocked = [[False for n in range(len(matrix[0]))] for m in range(len(matrix))]
```

#### enumerate for list
```
>>> elements = ('foo', 'bar', 'baz')
>>> for elem in elements:
...     print elem
... 
foo
bar
baz
>>> for count, elem in enumerate(elements):
...     print count, elem
... 
0 foo
1 bar
2 baz
```

#### empty list 
```
self.storedNodes != []
```

#### concat list
```
list1 + list2
```

#### item for dict
```
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```

#### set
Set is unordered, so not indexing. It is implemented as a hash table.

```
s1 = set()
s1.add(element1)
s1.remove(value1)
s1.pop() # often used to pop the last element remained

s2 = {e1, e2, e3}
s3 = s1 & s2 # intersection set
```

### data structure

#### stack
```
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
stack[-1] #the top element
```

#### queue

```
>>> from collections import deque
>>> queue = deque()
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> a = queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

#### heap

How to use PriorityQueue

```
from queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        counter = 0
        head = point = ListNode(0)
        q = PriorityQueue()
        for l in lists:
            if l:
                q.put((l.val,counter, l))
                counter += 1
        while not q.empty():
            val, _counter, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            if node:
                q.put((node.val, counter, node))
                counter += 1
        return head.next
        
```    

How to use heapq:

```
from heapq import heappush, heappop, heapify

class Node:
    def __init__(self, val):
        self.val = val


if __name__ == '__main__':
    # if Node can't be compared, let's have a 3-tuple list
    arr = [(2, 1, Node(3)), (3, 5,  Node(4)), (3, 2, Node(4))]
    heapify(arr)
    heappush(arr, (2, 4,  Node(5)))
    print(heappop(arr))
    print(heappop(arr))
    print(heappop(arr))
    print(heappop(arr))

```

Note: heapq pop returns smallest item

###check empty
`if matrix is None or len(matrix) == 0:`
or 
` if matrix == []`

### string

#### string <--> list

```
# string to char array:
s_list = list(str)

# list to str:
''.join(list)
```

#### char to number

```
ord(char)
```

### class variable

- Elements outside the __init__ method are static elements; they belong to the class.  
- Elements inside the __init__ method are elements of the object (self); they don't belong to the class.

```
class MyClass:
    static_elem = 123

    def __init__(self):
        self.object_elem = 456

c1 = MyClass()
c2 = MyClass()

# Initial values of both elements
>>> print c1.static_elem, c1.object_elem 
123 456
>>> print c2.static_elem, c2.object_elem
123 456

# Nothing new so far ...

# Let's try changing the static element
MyClass.static_elem = 999

>>> print c1.static_elem, c1.object_elem
999 456
>>> print c2.static_elem, c2.object_elem
999 456

# Now, let's try changing the object element
c1.object_elem = 888

>>> print c1.static_elem, c1.object_elem
999 888
>>> print c2.static_elem, c2.object_elem
999 456
```

```
solution = Solution()
solution.numSquares(3)
solution.numSquares(5)
solution.numSquares(33)
...
```

### dict

```
d = {}
d = {key:value}
d[new_key] = new_value

dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
dict['Age'] = 8; # update existing entry
dict['School'] = "DPS School"; # Add new entry

print "dict['Age']: ", dict['Age']
print "dict['School']: ", dict['School']

if 'key' in myDict:
    del myDict['key']
    
# Note: you cannot del in iteration of the dict

```

### sort

```
# in place list sort tuples based on second element:
my_list.sort(key=lambda x: x[1])

# create a new list
newList = sorted([('abc', 121),('abc', 231),('abc', 148), ('abc',221)], key=lambda x: x[1])

```

#### pass in comparator in sort

python3: use key=(firstItemToCmp, sec)

```
Sort word count. Data is represented by tuple: (word, count). 
1. sort by count in descending order
2. if count is same, sort them with alphebet order of word

>>> l = [('betty', 1), ('a', 1), ('butter', 2)]
>>> def custom_key(x):
...     return -x[1], x[0]
...
>>> l.sort(key=custom_key)
>>> l
[('butter', 2), ('a', 1), ('betty', 1)]
```

Or use the tradictional 1, -1 cmp:

```
from functools import cmp_to_key
nums = [1, 5, 2, 3, 5,7,98,43]
# x should be at right side of y if x < y (return 1)
nums.sort(key=cmp_to_key(lambda x, y: 1 if x < y else -1))
print(nums)

Output: [98, 43, 7, 5, 5, 3, 2, 1]
```

#### lexicographic order
python bydefault sort/compare is already lexicographic.  
What is that? https://chortle.ccsu.edu/java5/Notes/chap92/ch92_2.html  

```
A < a
ad < ca
abc < abcd
```

### split

split at first occurrence

```
>>> s = "123mango abcd mango kiwi peach"
>>> s.split("mango", 1)
['123', ' abcd mango kiwi peach']
```

### remove space 
```
# remove leading and trailing spaces
s = ' a kid  '
strip()
s = 'a kid'

lstrip
rstrip

# remove all spaces
s =  " ".join(s.split())
```


### read in input
need to take care of each "newline", usually use for loop

```
num = int(input())
    arr = []
    for _ in range(num):
        each = list(map(int,(input().rstrip().split())))
        each.pop(0)
        arr.append(each)

    print(arr)

```

### function

#### parameter
Default arguments:

```
def student(firstname, lastname ='Mark', standard ='Fifth'): 
     print(firstname, lastname, 'studies in', standard, 'Standard') 

# 1 positional argument 
student('John')  
  
# 3 positional arguments                          
student('John', 'Gates', 'Seventh')      
  
# 2 positional arguments   
student('John', 'Gates')                   
student('John', 'Seventh') 

 # 2 keyword arguments                  
student(firstname ='John', standard ='Seventh')   


```

Default parameter as in list:

```
def foo(val, arr=[]):
    arr.append(val)
    return arr
```
When using the function:

print(foo(1))  
[1]  
print(foo(2))  
[1, 2]  
This happens because the default value (an empty list) was evaluated once, when the function was compiled, then re-used on every call to the function. To get an empty list on every call, the code needs to be written like this:

```
def foo(val, arr=None):
    if arr is None:
        arr = []
    arr.append(val)
    return arr
```

Pass by Object reference:

In many cases these side effects are wanted, i.e. they are part of the functions specification. But in other cases, they are not wanted , they are hidden side effects. In this chapter we are only interested in the side effects, which change global variables, which have been passed as arguments to a function. 
Let's assume, we are passing a list to a function. We expect that the function is not changing this list. First let's have a look at a function which has no side effects. As a new list is assigned to the parameter list in func1(), a new memory location is created for list and list becomes a local variable.

```
>>> def func1(list):
...     print list
...     list = [47,11]
...     print list
... 
>>> fib = [0,1,1,2,3,5,8]
>>> func1(fib)
[0, 1, 1, 2, 3, 5, 8]
[47, 11]
>>> print fib
[0, 1, 1, 2, 3, 5, 8]
>>> 
```
This changes drastically, if we include something in the list by using +=. To show this, we have a different function func2() in the following example:

```
>>> def func2(list):
...     print list
...     list += [47,11]
...     print list
... 
>>> fib = [0,1,1,2,3,5,8]
>>> func2(fib)
[0, 1, 1, 2, 3, 5, 8]
[0, 1, 1, 2, 3, 5, 8, 47, 11]
>>> print fib
[0, 1, 1, 2, 3, 5, 8, 47, 11]
>>> 
```

#### various number of parameter

```
def formatString(stringTemplate, *args, **kwargs):
    # Replace any positional parameters
    for i in range(0, len(args)):
        tmp = '{%s}' % str(1+i)
        while True:
            pos = stringTemplate.find(tmp)
            if pos < 0:
                break
            stringTemplate = stringTemplate[:pos] + \
                             str(args[i]) + \
                             stringTemplate[pos+len(tmp):]
 
    # Replace any named parameters
    for key, val in kwargs.items():
        tmp = '{%s}' % key
        while True:
            pos = stringTemplate.find(tmp)
            if pos < 0:
                break
            stringTemplate = stringTemplate[:pos] + \
                             str(val) + \
                             stringTemplate[pos+len(tmp):]
 
    return stringTemplate
```
 
Here it is in action:

```
stringTemplate = 'pos1={1} pos2={2} pos3={3} foo={foo} bar={bar}'
print(formatString(stringTemplate, 1, 2))
pos1=1 pos2=2 pos3={3} foo={foo} bar={bar}
# note: bar=123 for **kwargs
print(formatString(stringTemplate, 42, bar=123, foo='hello'))
pos1=42 pos2={2} pos3={3} foo=hello bar=123
```


