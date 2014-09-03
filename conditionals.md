Conditional Expressions
-----------------------

Scala's if/else/else-if will look very familiar to those who have written in C-style languages before:

##### Python
```python
>>> x = 0
# Inline: expression_if_true if condition else expression_if_false
>>> foo = 1 if x > 0 else -1
>>> foo
-1
# Expressions broken across multiple lines
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

##### Scala
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

scala>

if (foo.isInstanceOf[String]) {
    print("Foo is a string!")
} else if (foo.isInstanceOf[Int]) {
    print("Foo is an int!")
} else {
    print("I dont know what foo is...")
}

Foo is a string!
```

While loops should look familiar as well:

##### Python
```python
n = 0
nlist = []
while n < 5:
    nlist.append(n)
    n += 1
>>> nlist
[0, 1, 2, 3, 4]
```

The following can actually be handled much better with a comprehension and a more functional approach, discussed below:

##### Scala
```scala
n: Int = 0

// ArrayBuffer is a mutable array that acts like Python lists.
scala> import scala.collection.mutable.ArrayBuffer
import scala.collection.mutable.ArrayBuffer

scala> var nlist = ArrayBuffer[Int]()
nlist: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer()

scala>

while (n < 5) {
    nlist += n
    n += 1
}

scala> nlist
res115: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(0, 1, 2, 3, 4)
}
```

For-loops and comprehensions, the latter of which is likely sorely missed by Python programmers writing Java. Scala supports a `for (variable <- expression)` syntax. Let's look at Python first:

##### Python
```python
foo = "Apple"
n = 0
for a in foo:
    n += 1
>>> n
5
```

##### Scala
```scala
scala> val foo = "Apple"

scala> var n = 0

scala>
for (x <- foo) {
    n += 1
}

scala> n
res140: n: Int = 5

// This would actually be better expressed in a single line
scala> n = 0

scala> for (x <- foo) n += 1

scala> n
res141: n: Int = 5
```

Python comprehensions are a very important part of writing idiomatic Python; Scala supports the same with the yield syntax:

##### Python
```python
>>> [f + 1 for f in [1, 2, 3, 4, 5]]
[2, 3, 4, 5, 6]
```

##### Scala
```scala
scala> for (f <- Array(1, 2, 3, 4, 5)) yield f + 1
res59: Array[Int] = Array(2, 3, 4, 5, 6)
```

Python has a very useful function called `zip` that will allow you to iterate over iterables at the same time. Scala will allow you to have multiple "generators" in an expression, which can replicate the zip behavior:

##### Python
```python
foo, bar = [1, 2, 3], ['a', 'b', 'c']
foobars = {}
for f, b in zip(foo, bar):
    foobars[b] = f
>>> foobars
{'a': 1, 'c': 3, 'b': 2}

# It's more Pythonic to use a comprehension
>>> {b: f for f, b in zip(foo, bar)}
{'a': 1, 'c': 3, 'b': 2}
```

##### Scala
```scala
val foo = Array(1, 2, 3)
val bar = Array("a", "b", "c")

import scala.collection.mutable.Map
// Let's go ahead and specify the types, since we know them
var foobars= Map[String, Int]()

for (f <- foo; b <- bar) foobars += (b -> f)
scala> foobars
res5: scala.collection.mutable.Map[String,Int] = Map(b -> 3, a -> 3, c -> 3)

// This is really powerful- we're not limited to two iterables
val baz = Array("apple", "orange", "banana")
val mapped = Map[String, (Int, String)]()
for (f <- foo; b <- bar; z <- baz) mapped += (z -> (f, b))
scala> mapped
res7: scala.collection.mutable.Map[String,(Int, String)] = Map(banana -> (3,c), orange -> (3,c), apple -> (3,c))

// It's worth noting that Scala also has an explicit zip method
val arr1 = Array(1, 2, 3)
val arr2 = Array(4, 5, 6)

scala> arr1.zip(arr2)
res240: Array[(Int, Int)] = Array((1,4), (2,5), (3,6))
```

Python's enumerate is a really nice language feature, and is mirrored by Scala's `zipWithIndex`:

##### Python
```python
>>> [(x, y) for x, y in enumerate(["foo", "bar", "baz"])]
[(0, 'foo'), (1, 'bar'), (2, 'baz')]
```

##### Scala
```scala
scala> for ((y, x) <- Array("foo", "bar", "baz").zipWithIndex) yield (x, y)
res27: Array[(Int, String)] = Array((0,foo), (1,bar), (2,baz))

// Note that simply calling zipWithIndex will return something similar (but with values // in reverse order)
scala> Array("foo", "bar", "baz").zipWithIndex
res31: Array[(String, Int)] = Array((foo,0), (bar,1), (baz,2))
```

Scala will allow "guard" expressions, which is the same as a control flow expression in Python:

##### Python
```python
foo = [1,2,3,4,5]
bar = [x for x in foo if x != 3]
>>> bar
[1, 2, 4, 5]
```

##### Scala
```scala
val foo = Array(1, 2, 3, 4, 5)
var bar = ArrayBuffer[Int]()
for (f <- foo if f != 3) bar += f
scala> bar
res136: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

// You can stack guards
scala> for (x <- (1 to 5).toArray if x != 2 if x != 3) yield x
res44: Array[Int] = Array(1, 4, 5)
```

Note that in many cases, it may be more concise to use `map` vs a for-comprehension:

##### Scala
```scala
scala> for (c <- Array(1, 2, 3)) yield c + 2
res56: Array[Int] = Array(3, 4, 5)

scala> Array(1, 2, 3).map(_ + 2)
res57: Array[Int] = Array(3, 4, 5)
```
