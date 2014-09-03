Maps
----

Scala has both immutable and mutable map types, whereas Python has the single reliable (and fast!) Dict. Here's a comparison of methods that effectively do the same thing for the two:

##### Python:
```python
fruit_count = {}
fruit_count = {"apples": 4, "oranges": 5, "bananas": 6}
>>> fruit_count["apples"]
4
>>> fruit_count.has_key("apples")
True
>>> fruit_count.get("melons", "peaches")
'peaches'
>>> fruit_count["melons"] = 2
>>> fruit_count.update({"peaches": 8, "pears": 4})
>>> fruit_count
{'peaches': 8, 'melons': 2, 'pears': 4, 'apples': 4, 'oranges': 5, 'bananas': 6}
>>> fruit_count.pop("apples")
4
>>> fruit_count
{'peaches': 8, 'melons': 2, 'pears': 4, 'oranges': 5, 'bananas': 6}
>>> fruit_count.keys()
['peaches', 'melons', 'pears', 'oranges', 'bananas']
>>> fruit_count.values()
[8, 2, 4, 5, 6]
```

##### Scala:
```scala
scala> val imm_fruit_count = Map("apples" -> 4, "oranges" -> 5, "bananas" -> 6)
imm_fruit_count: scala.collection.mutable.Map[String,Int] = Map(bananas -> 6, oranges -> 5, apples -> 4)

scala> imm_fruit_count("apples")
res219: Int = 4

scala> imm_fruit_count.contains("apples")
res220: Boolean = true

scala> imm_fruit_count.getOrElse("melons", "peaches")
res221: Any = peaches

scala> val mut_fruit_count = scala.collection.mutable.Map[String, Int]()
mut_fruit_count: scala.collection.mutable.Map[String,Int] = Map()

scala> mut_fruit_count("apples") = 4

scala> mut_fruit_count += ("oranges" -> 5, "bananas" -> 6)
res223: mut_fruit_count.type = Map(bananas -> 6, oranges -> 5, apples -> 4)

scala> mut_fruit_count
res224: scala.collection.mutable.Map[String,Int] = Map(bananas -> 6, oranges -> 5, apples -> 4)

scala> mut_fruit_count -= "apples"
res225: mut_fruit_count.type = Map(bananas -> 6, oranges -> 5)

scala> mut_fruit_count.keySet
res228: scala.collection.Set[String] = Set(bananas, oranges)

scala> mut_fruit_count.values
res229: Iterable[Int] = HashMap(6, 5)

// This is a nice feature of Scala Maps:
scala> val defaultMap = Map("foo" -> 1, "bar" -> 2).withDefaultValue(3)
defaultMap: scala.collection.immutable.Map[String,Int] = Map(foo -> 1, bar -> 2)

scala> defaultMap("qux")
res31: Int = 3
```

Scala will let you iterate over maps in a similar way as Python:

##### Python
```python
>>> foo = [k + str(v) for k, v in fruit_count.items()]
>>> foo
['peaches8', 'melons2', 'pears4', 'oranges5', 'bananas6']
```

##### Scala
```scala
scala> val foo = ArrayBuffer[String]()
foo: scala.collection.mutable.ArrayBuffer[String] = ArrayBuffer()

scala> for ((k, v) <- mut_fruit_count) foo += k.toString + v.toString

scala> foo
res237: scala.collection.mutable.ArrayBuffer[String] = ArrayBuffer(bananas6, oranges5)
```

A quick note: Scala has a SortedMap class that implements a tree map. The Python equivalent would be the OrderedDict in the collections module:

##### Python:
```python
import collections
foo = collections.OrderedDict(sorted({"apples": 4, "oranges": 5}.items()))
>>> foo
OrderedDict([('apples', 4), ('oranges', 5)])
```

##### Scala:
```scala
// PSA this is immutable
scala> val scores = scala.collection.immutable.SortedMap("oranges" -> 5, "apples" -> 4)
scores: scala.collection.immutable.SortedMap[String,Int] = Map(apples -> 4, oranges -> 5)
```



