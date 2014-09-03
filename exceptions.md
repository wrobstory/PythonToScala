Exceptions
----------

Exceptions are relatively straightforward in Scala, as they are in Python:

##### Python:
```python
def is_apple(fruit):
    if fruit != "apple":
        raise ValueError("Fruit is not apple!")

>>> is_apple("orange")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in is_apple
ValueError: Fruit is not apple!
```

##### Scala:
```scala
def is_apple(fruit:String) = {
    if (fruit != "apple") throw new IllegalArgumentException("Fruit is not apple!")
}

scala> is_apple("orange")
java.lang.IllegalArgumentException: Fruit is not apple!
  at .is_apple(<console>:16)
  ... 33 elided
```

Scala also has a try/catch/finally that behaves similarly to Python's try/except/finally:

##### Python:
```python
def check_fruit(fruit):
    try:
        is_apple(fruit)
        print('No exception raised...')
    except IOError:
        print("Oh no! IOError!")
    except ValueError as e:
        print(e.message)
    finally:
        print('This will excecute regardless of path.')

>>> check_fruit("apple")
No exception raised...
This will excecute regardless of path.
>>> check_fruit("orange")
Fruit is not apple!
This will excecute regardless of path.
```

##### Scala:
```scala
import java.io.IOException
def check_fruit(fruit:String) = {
  try {
    is_apple(fruit)
    print("No exception raised...")
  } catch {
    case ex: IllegalArgumentException => print(ex)
    case _: IOException => print("Oh no! IOException!")
  } finally {
    print("This will execute regardless of case.")
  }
}

scala> check_fruit("apple")
No exception raised...This will execute regardless of case.
scala> check_fruit("orange")
java.lang.IllegalArgumentException: Fruit is not apple!This will execute regardless of case.
```
