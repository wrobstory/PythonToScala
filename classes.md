Classes

Building classes with Scala is simpler than Java (woo!), but still with some added intricacies that you won't normally see when building Python classes. I highly recommend reading a bit on how Scala classes work, as there are a number of Java-like details that are worth knowing.

In the meantime, I'm going to show some simple classes that are comparable between the two, and leave it to the reader to investigate further:

##### Python
```python
class Closet:

    def __init__(self, skis, boots, bags):
        self.skis = skis
        self.boots = boots
        self.bags = bags

    def total_item_count(self):
        return self.skis + self.boots + self.bags


>>> mycloset = Closet(3, 4, 5)
>>> mycloset.skis
3
>>> mycloset.total_item_count()
12
>>> mycloset.skis = 10
>>> mycloset.total_item_count()
19
```

In Scala, use var to make all attributes mutable. Behind the scenes, Scala is creating getters and setters for each:

##### Scala
```scala
class Closet(var skis:Int, var boots:Int, var bags:Int){

    def total_item_count() = {
        // No "self" needed, and implicit return
        skis + boots + bags
    }
}

scala> val mycloset = new Closet(3, 4, 5)
mycloset: Closet = Closet@501959ff

scala> mycloset.skis
res61: Int = 3

scala> mycloset.total_item_count()
res62: Int = 12

scala> mycloset.skis = 10
mycloset.skis: Int = 10

scala> mycloset.total_item_count()
res63: Int = 19
```



