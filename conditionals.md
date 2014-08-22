Conditional expressions

Scala's if/else/else if will look very familiar to those who have written in C-style languages before.

##### Python:
```python
>>> x = 0
# Inline: expression_if_true if condition else expression_if_false
>>> foo = 1 if x > 0 else -1
>>> foo
-1
>> # Expressions broken across multiple lines
if x == 1:
    foo = 5
elif x == 0:
    foo = 6
>>> foo
6
>>>
if isinstance('foo', str):
    print('Foo is string')
else:
    print('Foo is not string')

Foo is string
```

##### Scala:
```scala
scala> val x = 0
x: Int = 0

// Inline: variable assignment expression
scala> val foo = if (x > 0) 1 else -1
foo: Int = -1

scala> var baz = 1
baz: Int = 1

// REPL paste mode
scala> :paste
// Entering paste mode (ctrl-D to finish)
// Kernighan & Ritchie brace style preferred for multi-line expressions
if (x == 0) {
  baz = 5
}
// Exiting paste mode, now interpreting.

scala> baz
res90: Int = 5
// But for simple expressions, try to keep them to one line
scala> if (x == 0) baz = 6

scala> baz
res94: Int = 6

scala> :paste
// Entering paste mode (ctrl-D to finish)

if (foo.isInstanceOf[String]) {
    print("Foo is a string!")
} else if (foo.isInstanceOf[Int]) {
    print("Foo is an int!")
} else {
    print("I dont know what foo is...")
}

// Exiting paste mode, now interpreting.

Foo is a string!
```

While loops should look familiar as well:

##### Python:
```python
n = 0
nlist = []
while n < 5:
    nlist.append(n)
    n += 1
>>> nlist
[0, 1, 2, 3, 4]
```

The following can actually be handled much better with a comprehension and a more functional approach, coming soon.

##### Scala:
```scala
n: Int = 0

// ArrayBuffer is a mutable array that acts like Python lists.
scala> import scala.collection.mutable.ArrayBuffer
import scala.collection.mutable.ArrayBuffer

scala> var nlist = ArrayBuffer[Int]()
nlist: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer()

scala> :paste
// Entering paste mode (ctrl-D to finish)

while (n < 5) {
    nlist += n
    n += 1
}

// Exiting paste mode, now interpreting.


scala> nlist
res115: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(0, 1, 2, 3, 4)
}
```

For loops and comprehensions. This is one thing that Scala brings to the Java world that is likely sorely missed by Python programmers writing in Java. Scala supports a `for (variable <- expression)` syntax. Let's look at Python first:

##### Python:
```python
foo = "Apple"
n = 0
for a in foo:
    n += 1
>>> n
5
```

##### Scala:
```scala
// Going to stop using the :paste mode, you get the gist
val foo = "Apple"
var n = 0
for (x <- foo) {
    n += 1
}
n

foo: String = Apple
n: Int = 5

// This would actually be better expressed in a single line
n = 0
for (x <- foo) n += 1
n

n: Int = 5
```

Python has a very useful function called `zip` that will allow you to iterate over iterables at the same time. Scala will allow you to have multiple "generators" in an expression, which can replicate the zip behavior:

##### Python:
```python
foo, bar = [1, 2, 3], ['a', 'b', 'c']
foobars = {}
for f, b in zip(foo, bar):
    foobars[b] = f
>>> foobars
{'a': 1, 'c': 3, 'b': 2}
```

##### Scala:
```scala
val foo = Array(1, 2, 3)
val bar = Array("a", "b", "c")

import scala.collection.mutable.Map
// Let's go ahead and specify the types, since we know them
var foobars:Map[String, Int] = Map()

for (f <- foo; b <- bar) foobars += (b -> f)
foobars

foobars: scala.collection.mutable.Map[String,Int] = Map(b -> 3, a -> 3, c -> 3)

// It's worth noting that Scala also has an explicit zip method
val arr1 = Array(1, 2, 3)
val arr2 = Array(4, 5, 6)
arr1.zip(arr2)

res240: Array[(Int, Int)] = Array((1,4), (2,5), (3,6))
```

Scala will allow "guard" expressions, which is the same as a control flow expression in Python.

Python:
```python
foo = [1,2,3,4,5]
bar = [x for x in foo if x != 3]
>>> bar
[1, 2, 4, 5]
```

##### Scala:
```
val foo = Array(1, 2, 3, 4, 5)
var bar = ArrayBuffer[Int]()
for (f <- foo if f != 3) bar += f
scala> bar
res136: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)
```

Above we saw a Python list comprehension- Scala supports the same with the yield syntax:

##### Python:
```python
>>> [f for f in foo]
[1, 2, 3, 4, 5]
```
Scala:
```scala
scala> for (f <- foo) yield f
res142: Array[Int] = Array(1, 2, 3, 4, 5)
```



