Arrays

As we've seen earlier, Scala's Array operates a bit differently than the Python List, and as such we need the ArrayBuffer class for arrays that are not fixed length.

Python:
```python
int_list = [1, 2, 3]
str_list = ["a", "b", "c"]
```

Scala:
```scala
val int_arr = Array(1, 2, 3)
val str_arr = Array("a", "b", "c")
```

Because Array is fixed length, the concept of initializing it to values exists:
Python:
```python
# These are contrived- you will rarely see the need for this in Python outside of NumPy
ten_zeroes = [0]*10
ten_none = [None]*10
```

Scala
```scala
val init_int = new Array[Int](10)
val init_str = new Array[String](10)

init_int: Array[Int] = Array(0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
init_str: Array[String] = Array(null, null, null, null, null, null, null, null, null, null)
```

ArrayBuffers work more like Python lists:
Python:
```python
int_list = []
int_list.append(1)
int_list.extend([2, 3, 4])
int_list.extend((5, 6, 7))
>>> int_list
[1, 2, 3, 4, 5, 6, 7]
>>> int_list.count(1)
>> # Closest thing to Scala trimEnd
>>> int_list = int_list[0:-5]
>>> int_list
[1, 2]
>>> int_list.insert(1, 5)
>>> int_list
[1, 5, 2]
>>> int_list.pop(1)
5
>>> int_list
[1, 2]
>>> int_list.reverse()
>>> int_list
[2, 1]
>>> int_list.sort()
>>> int_list
[1, 2]
>>> max(int_list)
2
>>> min(int_list)
1
```


Scala:
```scala
import scala.collection.mutable.ArrayBuffer

val int_arr = ArrayBuffer[Int]()
int_arr += 1
int_arr += (2, 3, 4)
int_arr ++= Array(5, 6, 7)

res182: int_arr.type = ArrayBuffer(1, 2, 3, 4, 5, 6, 7)

scala> int_arr.count(_ == 1)
res187: Int = 1

scala> int_arr.trimEnd(5)

scala> int_arr
res192: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

scala> int_arr.insert(1, 5)

scala> int_arr
res195: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 5, 2)

scala> int_arr.remove(1)
res196: Int = 5

scala> int_arr
res197: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

// Scala will also let you be more flexible with multiple insert/remove
scala> int_arr.insert(1, 5, 6)

scala> int_arr
res199: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 5, 6, 2)

scala> int_arr.remove(1, 2)

scala> int_arr
res201: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

scala> int_arr.reverse
res205: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(2, 1)

scala> int_arr.max
res210: Int = 2

scala> int_arr.min
res211: Int = 1

scala> int_arr.reverse.sorted
res215: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)
```

Though we already covered for-statements and sequence traversal, its worth noting Scala's `until` operator that works a lot like Python's range:

Python:
```python
foo = [f for f in range(0, 10, 1)]
>>> foo
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
foo = [f for f in range(0, 10, 2)]
>>> foo
[0, 2, 4, 6, 8]
```

Scala:
```scala
scala> val foo = for (x <- 0 until 10) yield x
foo: scala.collection.immutable.IndexedSeq[Int] = Vector(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

scala> val foo = for (x <- 0 until (10, 2)) yield x
foo: scala.collection.immutable.IndexedSeq[Int] = Vector(0, 2, 4, 6, 8)

// Scala also has a "to" operator that creates an inclusive range
scala> 0 to (10, 2)
res22: scala.collection.immutable.Range.Inclusive = Range(0, 2, 4, 6, 8, 10)

scala> 0 until (10, 2)
res23: scala.collection.immutable.Range = Range(0, 2, 4, 6, 8)
```

It's worth noting the comprehension syntax again, including the "guard" clause:

Python:
```python
foo = [x + "qux" for x in ["foo", "bar", "baz"] if x != "foo"]
>>> foo
['barqux', 'bazqux']
```

Scala:
```scala
scala> val foo = for (x <- ArrayBuffer("foo", "bar", "baz") if x != "foo") yield x + "qux"
foo: Array[String] = Array(barqux, bazqux)

// Note that the comprehension returns the type that is fed to it
scala> val foo = for (x <- ArrayBuffer("foo", "bar", "baz") if x != "foo") yield x + "qux"
foo: scala.collection.mutable.ArrayBuffer[String] = ArrayBuffer(barqux, bazqux)
```

A quick note that Scala supports multi-dimensional arrays out of the box, whereas in Python, you are really best off using the NumPy library.

Scala:
```scala
scala> val multdim = Array.ofDim[Int](3, 4)
multdim: Array[Array[Int]] = Array(Array(0, 0, 0, 0), Array(0, 0, 0, 0), Array(0, 0, 0, 0))

scala> multdim(0)(2) = 15

scala> multdim
res217: Array[Array[Int]] = Array(Array(0, 0, 15, 0), Array(0, 0, 0, 0), Array(0, 0, 0, 0))
```
