Functions

Scala functions will actually look relatively familiar to Python programmers, except that you need to specify the type of the arguments you're passing to the func: 

Python:
```python
def concat_num_str(x, y):
    if not isinstance(x, str):
        x = str(x)
    return x + y
>>> concat_num_str(1, "string")
'1string'
```

Note that Scala does not require a return statement:

Scala: 
```scala
def concat_num_str(x:Int, y:String) = x.toString + y
scala> concat_num_str(1, "string")
res146: String = 1string

// What happens if we try to pass the incorrect type?
scala> concat_num_str("string", num)
<console>:19: error: type mismatch;
 found   : String("string")
 required: Int
              concat_num_str("string", num)
                             ^
<console>:19: error: not found: value num
              concat_num_str("string", num)
```

If using multiple expressions, use a bracketed block:
Scala:
```scala
import scala.collection.mutable.Map
val str_arr = Array("apple", "orange", "grape")

def len_to_map(arr:Array[String]) = {
    var lenmap:Map[String, Int] = Map()
    for (a <- arr) lenmap += (a -> a.length)
    lenmap
}

scala> len_to_map(str_arr)
res149: scala.collection.mutable.Map[String,Int] = Map(orange -> 6, apple -> 5, grape -> 5)
```

With Scala, you can specify a return type, and *have* to do so in recursive funcs: 
Scala: 
```scala
def factorial(n: Int): Int = if (n <= 0) 1 else n * factorial(n - 1)
scala> factorial(5)
res152: Int = 120
```

Default and named arguments should be very familiar for Python users: 
Python
```python
def make_arr(x, y, fruit="apple", drink="water"):
    return [x, y, fruit, drink]
>>> make_arr("orange", "banana")
['orange', 'banana', 'apple', 'water']
>>> make_arr("orange", "banana", "melon")
['orange', 'banana', 'melon', 'water']
>>> make_arr("orange", "banana", drink="coffee")
['orange', 'banana', 'apple', 'coffee']
```
Scala
```scala
def make_arr(x:String, y:String, fruit:String = "apple", drink:String = "water") = Array(x, y, fruit, drink)

scala> make_arr("orange", "banana")
res154: Array[String] = Array(orange, banana, apple, water)

scala> make_arr("orange", "banana", "melon")
res155: Array[String] = Array(orange, banana, melon, water)

scala> make_arr("orange", "banana", drink="coffee")
res156: Array[String] = Array(orange, banana, apple, coffee)

// As with Python, non-named parameters need to be supplied before named ones
scala> make_arr("orange", drink="coffee", "banana")
<console>:19: error: not enough arguments for method make_arr: (x: String, y: String, fruit: String, drink: String)Array[String].
Unspecified value parameter y.
              make_arr("orange", drink="coffee", "banana")
```

Scala supports variable arguments in a similar way to Python's *args, but with a little less flexibility- Scala just knows that its being given a sequence of arguments that it can operate on. 

Python:
```python
def sum_args(*args):
    return sum(args)

>>> sum_args(1, 2, 3, 4, 5)
15
```

Scala:
```scala
def sum_args(args:Int*) = args.sum
scala> sum_args(1, 2, 3, 4, 5)
res159: Int = 15
```

As with Python, you can't just pass in a sequence- it needs to be deconstructed first: 
Python:
```
>>> sum_args([1, 2, 3])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in sum_args
TypeError: unsupported operand type(s) for +: 'int' and 'list'

>>> sum_args(*[1, 2, 3])
6
```

Scala: 
```scala
scala> sum_args(Array(1, 2, 3))
<console>:17: error: type mismatch;
 found   : Array[Int]
 required: Int
              sum_args(Array(1, 2, 3))

scala> sum_args(Array(1, 2, 3): _*)
res161: Int = 6
```

I should note here that Scala does have a special "Procedure" type function that returns no value, wherein the `=` sign is omitted:
Scala:
```scala
def proc_func(x:String, y:String) {print(x + y)}
proc_func("x", "y")
```
