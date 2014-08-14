Arithmetic

Scala and Python largely share arithmetic operations. Behind the scenes, they are both using methods to implement the operaters- Scala uses the actual operator symbol, rather than an alphanumeric character: 
Python
```python
>>> foo = 1 
# What's happening behind the scenes?
>>> foo.__add__(4)
5
```

```scala
scala> val foo = 1
foo: Int = 1

scala> foo + 1
res72: Int = 2
// What's happening behind the scenes: 
scala> foo.+(1)
res73: Int = 2
```

