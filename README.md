Demystifying-Python
===================

A Quick(ish) tutorial for Rubyists curios about learning Python.

##More similarities than differences

Both languages are high-level, dynamically typed, and object-oriented.Overall, they are pretty similar. But, they evolved in slightly different directions. 

The same basic rules apply:

```
In [1]: 1 + 1
Out[1]: 2

In [2]: print "Hello World"
Hello World

In [3]: x = "some stuff"

In [4]: print x
some stuff
```

The syntax is different in a few small places: 
* manditory parenthesis
* no implicit returns
* whitespace instead of end statements
* colons
* different elsif
* different && and || opperators
* uppercase true and false

```
In [5]: def func(x,y,z):
   ...:     return x+y+z
   ...: 

In [6]: func(1,2,3)
Out[6]: 6

In [7]: def func2(a):
   ...:     if a <= 0:
   ...:         return "negative"
   ...:     elif a>0 and a<5:
   ...:         return "less than 5"
   ...:     else:
   ...:         return "more than 5"
   ...:     


In [8]: func2(3)
Out[8]: 'less than 5'

In [9]: func2(-1)
Out[9]: 'negative'

In [10]: func2(10)
Out[10]: 'more than 5'

In [11]: True or False
Out[11]: True

In [12]: True and False
Out[12]: False
```

But the idea is the same:
* Do as much as possible in as few words as possible
* Emphasize readability and programmer productivity

###Syntactical tricks

Most syntactical tricks you can do in Ruby, you can also do in Python.Here is a [good list of stuff you CAN do in Python](http://sahandsaba.com/thirty-python-language-features-and-tricks-you-may-not-know.html)

## Datatypes

* No symbols
* Lists == Arrays (with better slicing)
* Dictionaries == Hashes (with JSON-y syntax, rather than hash rockets)
* Tuples
* Sets

### Lists
```
In [13]: list = [0,1,2,3,4,5,6,7,8,9,'string', True, None]

In [14]: list[0]
Out[14]: 0

In [15]: list[3:8]
Out[15]: [3, 4, 5, 6, 7]

In [16]: list[:8]
Out[16]: [0, 1, 2, 3, 4, 5, 6, 7]

In [17]: list[8:]
Out[17]: [8, 9, 'string', True, None]

In [18]: list[-1]
#it didn't return anything

In [19]: list[-2]
Out[19]: True

In [20]: list[::2]
Out[20]: [0, 2, 4, 6, 8, 'string', None]

In [21]: list[::-2]
Out[21]: [None, 'string', 8, 6, 4, 2, 0]
```

###Dictionaries
```
In [22]: dict = {"a":1, "b":2, "c":[4,5,6]}

In [23]: dict["a"]
Out[23]: 1

In [24]: dict["c"]
Out[24]: [4, 5, 6]

In [25]: dict = {"a":1, "b":2, [1,2,3]:[4,5,6]}
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-22-e5bc73dbf621> in <module>()
----> 1 dict = {"a":1, "b":2, [1,2,3]:[4,5,6]}

TypeError: unhashable type: 'list'

```
###Tuples
* The same as lists, but immutable.
* Tuples are good for passing series of arguments around without fear of the order being mutated. 
* They also have faster load time because they are immutable.


```
In [26]: tup = (1,2,3)

In [27]: tup[0]
Out[27]: 1

In [28]: tup.pop()
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-29-9e226b0399e4> in <module>()
----> 1 tup.pop()

AttributeError: 'tuple' object has no attribute 'pop'

In [29]: del list
# Python is less strict about reserved words. Deleting the list variable here so we can use the list function.
# You can't delete variables in Ruby...You have to set the variable equal to nil, and wait for the garbage collector to pick it up.

In [30]: list(tup)
Out[30]: [1, 2, 3]

In [31]: tup
Out[31]: (1, 2, 3)

In [32]: list(tup).pop()
Out[32]: 3

```

###Sets

Sets are unordered collections of unique values. They also have faster load times than lists.

```
In [33]: a_set = {1,2,3,4,4,4,4,4,4,4}

In [34]: a_set
Out[34]: {1, 2, 3, 4}

In [35]: a_set.add(5)

In [36]: a_set
Out[36]: {1, 2, 3, 4, 5}

In [37]: b_set = set([3,3,3,3,3,3,3,3,3,3, "aaaaaaaaaa"])

In [38]: b_set
Out[38]: {3, 'aaaaaaaaaa'}

In [39]: a_set.union(b_set)
#or... a_set | b_set
Out[39]: {1, 2, 3, 4, 5, 'aaaaaaaaaa'}

In [40]: a_set.difference(b_set)
#or... a_set - b_set
Out[40]: {1, 2, 4, 5}

In [41]: a_set.intersection(b_set)
#or... a_set & b_set
Out[41]: {3}
```

##Living without blocks
One undeniable drawback of Python: no blocks.
You're forced to loop through things the old fashion way...with for/while loops:

```
In [42]: my_list = [1,2,3,4,5,6,7,8,9,10]

In [43]: for number in my_list:
   ....:     print number*number
   ....:     
1
4
9
16
25
36
49
64
81
100

In [44]: i = 0

In [45]: while i < my_list[-1]:
   ....:     print i
   ....:     i +=1
   ....:     
0
1
2
3
4
5
6
7
8
9
```
Keep in mind that, like Ruby, Python has a fantastic library to help you do what you want to do...it just might not be as obvious.

For example, `array.each_with_index{|v,i| ...} == for i,v in enumerate(list): ...`

This can make things a pain in the ass sometimes, but can also make things easier to reason about when reading nested loops. 

In addition, Python has some "special sauce" to help make things easier.

###Comprehensions
Syntactic sugar for making complicated lists/dictionaries/sets on the fly.

```
In [49]: [x for x in range(10)]
Out[49]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

In [50]: [x for x in range(5,10)]
Out[50]: [5, 6, 7, 8, 9]

In [51]: [x for x in range(2,10,2)]
Out[51]: [2, 4, 6, 8]

In [52]: comp = [x for x in range(2,13,2) if x%3==0]

In [53]: comp
Out[53]: [6,12]

In [54]: [x**x for x in range(2,10,2)]
Out[54]: [4, 256, 46656, 16777216]

In [55]: suits = ['Hearts','Spades','Clubs','Diamonds']

In [56]: values = ['Ace',2,3,4,5,6,7,8,9,10,'Jack','Queen','King']

In [57]: [(value, suit) for suit in suits for value in values]
Out[57]: 
[('Ace', 'Hearts'),
 (2, 'Hearts'),
 (3, 'Hearts'),
 (4, 'Hearts'),
 (5, 'Hearts'),
 (6, 'Hearts'),
 (7, 'Hearts'),
 (8, 'Hearts'),
 (9, 'Hearts'),
 (10, 'Hearts'),
 ('Jack', 'Hearts'),
 ('Queen', 'Hearts'),
 ('King', 'Hearts'),
 ('Ace', 'Spades'),
 (2, 'Spades'),
 (3, 'Spades'),

# and so forth...
]

In [58]: dict = {"key1":"val1", "key2":"val2", "key3":"val3"}

In [59]: {val:key for key, val in dict.items()}
Out[59]: {'val1': 'key1', 'val2': 'key2', 'val3': 'key3'}
```

###Generators

Generators are weird, and I don't understand them well. Here's what the [docs](https://docs.python.org/2/howto/functional.html#generator-expressions-and-list-comprehensions) say:

```
When you call a function, it gets a private namespace where its local variables are created. When the function reaches a return statement, the local variables are destroyed and the value is returned to the caller. A later call to the same function creates a new private namespace and a fresh set of local variables. But, what if the local variables weren’t thrown away on exiting a function? What if you could later resume the function where it left off? This is what generators provide; they can be thought of as resumable functions.
```
In other words, generators are single-use iteration tools that remember where you left off, and can pick up in that place whenever you need it.

```
In [60]: def generate_sq(n):
   ....:     for i in range(n):
   ....:         yield i**2
   ....:         

In [61]: gen = generate_sq(5)

In [62]: gen
Out[62]: <generator object generate_sq at 0x102a06e10>

In [63]: next(gen)
Out[63]: 0

In [64]: next(gen)
Out[64]: 1

In [65]: next(gen)
Out[65]: 4

In [66]: next(gen)
Out[66]: 9

In [67]: next(gen)
Out[67]: 16

In [68]: next(gen)
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-71-8a6233884a6c> in <module>()
----> 1 next(gen)

StopIteration: 
```
Why would you use this? Something to do with performance. I can't think of any good examples, but probably useful where you'd ordinarily generate a new list for one value several times. 

Ruby has "fibers", which are the same thing (I think)

##Functional programmning, "first class" functions...and decorators

In Python, you can pass functions as arguments to other functions.

First class functions exist in Ruby (kind of), and in JavaScript.

Let's say we want to time how long it takes to run a function:
```
In [69]: import time

In [70]: def time_it(func, args):
   ....:     before = time.time()
   ....:     func(args)
   ....:     after = time.time()
   ....:     print after - before
   ....:     

In [71]: def stuff(n):
   ....:     for x in xrange(n):
   ....:         x**2
   ....:         

In [72]: time_it(stuff, 5)
8.10623168945e-06

In [73]: time_it(stuff, 5000)
0.00114893913269

In [74]: time_it(stuff, 50000)
0.00881218910217

In [75]: time_it(stuff, 5000000)
0.403421878815
```

Let's say we want to permanently alter stuff's functionality:

```
In [76]: def time_wrapper(func):
   ....:     def new_func(args):
   ....:        before = time.time()
   ....:        func(args)
   ....:        after = time.time()
   ....:        print after - before
   ....:     return new_func
   ....: 

In [77]: stuff = time_wrapper(stuff)

In [78]: stuff(5)
6.91413879395e-06
```

Another way to write `In [77]`:
```
In [79]: @time_wrapper
   ....: def other_stuff(x):
   ....:     for number in range(x):
   ....:         number * 9 + 8
   ....:         

In [80]: other_stuff(10)
8.10623168945e-06
```

If you want to get fancy, you can also pass arguments to your decorators:

```
In [81]: def decorate_with_args(arg1, arg2):
   ....:     def wrap(func):
   ....:         print "inside wrap"
   ....:         print arg1, arg2
   ....:         def wrapped_func(*args):
   ....:             print "inside wrapped_func"
   ....:             print "decorator args:", arg1, arg2
   ....:             func(*args)
   ....:         return wrapped_func
   ....:     return wrap
   ....: 


In [82]: @decorate_with_args("woo", "hoo")
  .....: def more_stuff(a,b,c):
  .....:     print a,b,c
  .....:     
inside wrap
woo hoo

In [83]: more_stuff("yolo", "oloy", "qwerty")
inside wrapped_func
decorator args: woo hoo
yolo oloy qwerty

In [84]: more_stuff(1,2,3)
inside wrapped_func
decorator args: woo hoo
1 2 3
```
##Classes

A lot of rubyists say that Python is not object oriented. They're wrong. 

Syntax is pretty similar, but there are some key differences:
* No @s. Everything is self.whatever
* No attr_reader, attr_writer, attr_accessor. Everything is public. Deal with it.
* Magic methods: Like in Ruby, Python objects inherit behavior from a root object. You can overwrite these, but it looks less pretty.

```
In [85]: class OrangeTree(object):
   .....:     def __init__(self, n_of_oranges):
   .....:         self.oranges = n_of_oranges
   .....:     def orange_indeces(self):
   .....:         return range(self.oranges)
   .....:     def __str__(self):
   .....:         return "this tree has {0} oranges".format(self.oranges)
   .....:     

In [86]: orange = OrangeTree(5)

In [87]: orange.oranges
Out[87]: 5

In [88]: orange.orange_indeces
Out[88]: <bound method OrangeTree.orange_indeces of <__main__.OrangeTree object at 0x101ebf850>>

In [89]: orange.orange_indeces()
Out[89]: [0, 1, 2, 3, 4]

In [90]: orange
Out[90]: <__main__.OrangeTree at 0x101ebf850>

In [91]: print orange
this tree has 5 oranges
```
##So, why use Python? For performance (kind of) and Libraries

For the most part, Python is just a marginally uglier version of Ruby. In many cases, solving a problem in Ruby is faster, and ends up being easier on the eyes. However, I generally think that Python looks cleaner and is easier to reason about when solving math-heavy problems.

In any case, Python is fairly popular in data-intensive disciplines (academia, finance, data science). As a result, Pythong has some fantastic data-crunching tools.

###Cython
I've never used this, but it looks incredibly useful in some circumstances.

Cython lets you (optionally) statically type variables, and compiles the Python code down to C code.

In some circumstances, you can make your code run about as fast as C code.

```
# Regular Python
def fib(n):
    a,b = 1,1
    for i in range(n):
        a,b = a+b, a
    return a

#Cython... supposedly 70x faster
def cfib(int n):
    cdef int i, a, b
    a,b = 1,1
    for i in range(n):
        a, b = a+b, a
    return a
```

Several data-crunching libraries are written largely in Cython, such as Numpy, SciPy, pandas, and scikit-learn

###Numpy & SciPy

If you ever need to use multi-dimensional arrays (in the mathematical sense, not the Ruby sense), Numpy is where it's at.

```
In [92]: import numpy as np

In [93]: list1 = [0,1,2,3,4,5,6,7,8,9]

In [94]: array1 = np.array(list1)

In [95]: array1
Out[95]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

In [96]: array1 + 5
Out[96]: array([ 5,  6,  7,  8,  9, 10, 11, 12, 13, 14])

In [97]: array1 * 5
Out[97]: array([ 0,  5, 10, 15, 20, 25, 30, 35, 40, 45])

In [98]: array2 = array1 * 5

In [99]: array2 - array1
Out[99]: array([ 0,  4,  8, 12, 16, 20, 24, 28, 32, 36])
```

This also works for n-dimensional arrays.

The library also comes with a bunch of awesome functions that help with n-d array and linear algebra computations.

Numpy is included in the SciPy environment, which also contains libraries for plotting data (matplotlib), k-means clustering (cluster), machine learning (scikit-learn), and other awesome stuff.

###Pandas

If you're used to conducting data analysis with spreadsheets, pandas should seem pretty intuative. pandas sits on top of the SciPy environment, and groups data into "data frames". This allows you to perform  operations on a DB as if they were organized by column and row. You can also do v-lookup-style operations, run multiple regressions. It also makes importing/exporting data and dealing with timestamps a lot easier.

More importly, it's a beast for cleaning up and reshaping data.

A seperate library, pandasql, allows you to make SQL queries on dataframes.

[More on Pandas](http://pandas.pydata.org/index.html)

###NLTK

Natural Language ToolKit. If you ever want to perform language analysis, look no further

Just like the Alchemy API, but free and more dynamic.

[More on NLTK](http://www.nltk.org/)
[Free Book](http://victoria.lviv.ua/html/fl5/NaturalLanguageProcessingWithPython.pdf)

###IPython
IPython is an awesome Python REPL...it is far better than anything Ruby has ever come up with. 

Also, it's got [this awesome thing](http://ipython.org/notebook.html).

###Other Cool libraries I'm too lazy to write about
* Twisted
* Flask == Sinatra
* Django == Rails


##Package Management

One undeniable negative of Python: package management sucks. It's often a major pain in the ass to download, install, and use these libraries. Thankfully, there are a few popular distributions out there that simplify the process.

I'm a big fan of [Anaconda](https://store.continuum.io/cshop/anaconda/) (free download). Here's a list of all the [packages included](http://docs.continuum.io/anaconda/pkg-docs.html).

##Version Management

Python 3 is the wave of the future. Unfortunately, Python 3 is not backwards compatable with Python 2. Therefore, a large chunk of Python coders are still using Python 2.7. I still use 2.7 because the Anaconda distribution is better for that version. 

In any case, the differences aren't terribly significant, so I feel comfortable mirating to 3.4 whenever.

[More info on the differences between Python 2.7 and Python 3.x](http://nbviewer.ipython.org/github/rasbt/python_reference/blob/master/tutorials/key_differences_between_python_2_and_3.ipynb)

##More Resources

* [Dive Into Python](http://www.diveintopython3.net/)
* [Python's Awesome Documentation](https://docs.python.org/2/)
* [Kahn Academy's Python/Coding Tutorial](https://www.youtube.com/watch?v=husPzLE6sZc&list=PLJR1V_NHIKrCkswPMULzQFHpYa57ZFGbs)



