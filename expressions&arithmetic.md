Expressions and Arithmetic
--------------------------

Expressions should look familiar, though you should note that Scala has both `val` (immutable) and `var` (mutable) bindings. Try to use immutability whenever possible:

##### Scala
```scala
scala> val foo = 1
foo: Int = 1

scala> foo = 2
<console>:8: error: reassignment to val
       foo = 2
           ^

scala> var foo = 1
foo: Int = 1

scala> foo = 2
foo: Int = 2
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
