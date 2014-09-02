#Python to Scala:

##Variables

Python:
```python
>>> foo = "Apples"
>>> baz = foo + " and Oranges."
>>> baz
'Apples and Oranges.'
>>> baz = "Only Grapes."
```


Scala:
```scala
scala> val foo = "Apples"
foo: String = Apples

scala> val baz = foo + " and Oranges."
baz: String = Apples and Oranges.


scala> baz
res60: String = Apples and Oranges.


// In Scala, vals are immutable
scala> baz = "Only Grapes."
<console>:13: error: reassignment to val
       baz = "Only Grapes."


// Create a var instead
scala> var baz = "Apples and Oranges."
baz: String = Apples and Oranges.

scala> baz = "Only Grapes."
baz: String = Only Grapes.

scala> var one = 1
one: Int = 1

scala> one += 1

scala> one
res21: Int = 2
```

Scala will also let you specify the type for the compiler:

```scala
scala> val foo: String = "Apples"
foo: String = Apples
```

Python and Scala will both let you perform multiple assignment. However, be careful with Python and pass by reference! You'll usually want to unpack rather than perform multiple assignment.

Scala:
```scala
scala> val foo, bar = Array(1, 2, 3)
foo: Array[Int] = Array(1, 2, 3)
bar: Array[Int] = Array(1, 2, 3)

// foo and bar reference different pieces of memory; changing one will not change the other.
scala> bar(0) = 4

scala> bar
res70: Array[Int] = Array(4, 2, 3)

scala> foo
res71: Array[Int] = Array(1, 2, 3)
```

The same can be achieved with Python unpacking:
```python
>>> foo, bar = [1, 2, 3], [1, 2, 3]
# Are they referencing the same memory?
>>> foo is bar
False
# What happens when you change bar?
>>> bar[0] = 4
>>> bar
[4, 2, 3]
>>> foo
[1, 2, 3]


# You *can* assign both foo and bar the same value, but they reference the same memory!
>>> foo = bar = [1, 2, 3]
>>> foo is bar
True
>>> bar[0] = 4
>>> bar
[4, 2, 3]
>>> foo
[4, 2, 3]
```

Scala and Python largely share arithmetic operations. Behind the scenes, they are both using methods to implement the operaters- Scala uses the actual operator symbol, rather than an alphanumeric character:

##### Python
```python
>>> foo = 1
# What's happening behind the scenes?
>>> foo.__add__(4)
5
```

##### Scala
```scala
scala> val foo = 1
foo: Int = 1

scala> foo + 1
res72: Int = 2
// What's happening behind the scenes:
scala> foo.+(1)
res73: Int = 2
```
