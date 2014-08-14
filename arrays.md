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
