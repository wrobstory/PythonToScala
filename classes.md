Classes

Building classes with Scala is simpler than Java (woo!), but still with some added intricacies that you won't normally see when building Python classes. I highly recommend reading a bit on how Scala classes work, as there are a number of Java-like details that are worth knowing.

In the meantime, I'm going to show some simple classes that are comparable between the two, and leave it to the reader to investigate further:

##### Python
```python
class Automobile(object):

    def __init__(self, wheels=4, engine=1, lights=2):
        self.wheels = wheels
        self.engine = engine
        self.lights = lights

    def total_parts(self):
        return self.wheels + self.engine + self.lights

    def remove_wheels(self, count):
        if (self.wheels - count) < 0:
            raise ValueError('Automobile cannot have fewer than 0 wheels!')
        else:
            self.wheels = self.wheels - count
            print('The automobile now has {} wheels!').format(self.wheels)


>>> car = Automobile()
>>> car.wheels
3
>>> car.total_parts()
7
>>> car.wheels = 6
>>> car.total_parts()
9
>>> car.remove_wheels(7)
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-30-24207883207a> in <module>()
----> 1 car.remove_wheels(7)

<ipython-input-27-41c5871dc8ce> in remove_wheels(self, count)
     11     def remove_wheels(self, count):
     12         if (self.wheels - count) < 0:
---> 13             raise ValueError('Automobile cannot have fewer than 0 wheels!')
     14         else:
     15             self.wheels = self.wheels - count

ValueError: Automobile cannot have fewer than 0 wheels!

>>> car.remove_wheels(2)
The automobile now has 4 wheels!
```

In Scala, use var to make all attributes mutable. Behind the scenes, Scala is creating getters and setters for each:

##### Scala
```scala
class Automobile(var wheels:Int = 4, var engine:Int = 1, var lights:Int = 2 ){

    def total_parts() = {
        // No "self" needed, and implicit return
        wheels + engine + lights
    }

    // Purely side-effecting function, no "=" needed
    def remove_wheels(count:Int) {
        if (wheels - count < 0) {
            throw new IllegalArgumentException("Automobile cannot have fewer than 0 wheels!")
        } else {
            wheels = wheels - count
            println(s"Auto now has $wheels wheels!")
        }
    }
}

scala> val car = new Automobile()
car: Automobile = Automobile@77424e9

scala> car.wheels
res64: Int = 4

scala> car.total_parts()
res65: Int = 7

scala> car.wheels = 6
car.wheels: Int = 6

scala> car.total_parts()
res66: Int = 9

scala> car.remove_wheels(7)
java.lang.IllegalArgumentException: Automobile cannot have fewer than 0 wheels!
  at Automobile.remove_wheels(<console>:19)
  ... 32 elided

scala> car.remove_wheels(2)
Auto now has 4 wheels!
```

In Scala, if you define a constructor field as val (immutable), you get a getter but not a setter. This is roughly comparable to defining your own property getter/setters on a Python class (for a great rundown of Python properties and descriptors, check out Chris Beaumont's [Python Descriptors Demystified](http://nbviewer.ipython.org/gist/ChrisBeaumont/5758381/descriptor_writeup.ipynb)):

##### Python
```python
class Automobile(object):

    def __init__(self, wheels=4):
        # The underscore is convention, but not enforced
        self._wheels = wheels

    @property
    def wheels(self):
        return self._wheels

    @wheels.setter
    def wheels(self, count):
        raise ValueError('This value is immutable!')

>>> car = Automobile()
>>> car.wheels
4
>>> car.wheels = 5
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-26-f07fada773fb> in <module>()
----> 1 car.wheels = 5

<ipython-input-23-87368b68789b> in wheels(self, count)
     11     @wheels.setter
     12     def wheels(self, count):
---> 13         raise ValueError('This value is immutable!')

ValueError: This value is immutable!
```

##### Scala
```scala
class Automobile(val wheels:Int = 4){}

scala> val car = new Automobile()
car: Automobile = Automobile@64284ba3

scala> car.wheels
res67: Int = 4

scala> car.wheels = 5
<console>:12: error: reassignment to val
       car.wheels = 5
                  ^
```

Like Java, Scala also allows you to define fields as `private`, which prevents getters/setters from being generated and only allows the field to be accessed within the class. This behavior can be replicated in Python, but you won't often see this pattern actually being used in Python programs- it is understood that class attributes leading with an underscore are "private" and should not be used:

##### Python
```python
class Automobile(object):

    def __init__(self, wheels=4):
        # The underscore is convention, but not enforced
        self._wheels = wheels

    @property
    def wheels(self):
        raise ValueError('You cannot access this value!')

    @wheels.setter
    def wheels(self, count):
        raise ValueError('You cannot access this value!')

>>> car.wheels
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-41-d267b674bbda> in <module>()
----> 1 car.wheels

<ipython-input-39-73ff0f17068d> in wheels(self)
      7     @property
      8     def wheels(self):
----> 9         raise ValueError('You cannot access this value!')
     10
     11     @wheels.setter

ValueError: You cannot access this value!

>>> car.wheels = 5
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-42-f07fada773fb> in <module>()
----> 1 car.wheels = 5

<ipython-input-39-73ff0f17068d> in wheels(self, count)
     11     @wheels.setter
     12     def wheels(self, count):
---> 13         raise ValueError('You cannot access this value!')

ValueError: You cannot access this value!
```

##### Scala
```scala
class Automobile(private val wheels:Int = 4){}

scala> car.wheels
<console>:11: error: value wheels in class Automobile cannot be accessed in Automobile
              car.wheels
                  ^

scala> car.wheels = 5
<console>:13: error: value wheels in class Automobile cannot be accessed in Automobile
val $ires4 = car.wheels
```

Staticmethods in Scala are handled via "companion objects" for classes, which are named the same as the class itself. Objects are an entire topic of study for the Scala language- I am just touching on them as they related to Python's `staticmethod`, but I recommend that you do some reading on how objects are used in Scala. Also demonstrated in this example is how object fields can be used to mirror Python's class-level attributes:

##### Python
```python
class Automobile(object):

    wheels = 4
    lights = 2

    def __init__(self, name):
        self.name = name

    @staticmethod
    def print_uninst_str():
        print("No 'self' passed to this method, and no instantiation."
              " It's static!")

>>> Automobile.print_uninst_str()
No 'self' passed to this method, and no instantiation. It's static!
>>> Automobile.wheels
4
>>> Automobile.wheels = 5
>>> Automobile.wheels
5
```

##### Scala
```scala
class Automobile(var name:String){}

object Automobile {
    var wheels = 4
    var lights = 2
    def print_uninst_str() = "No 'self' passed to this method, and no instantiation. It's static!"
}

scala> Automobile.print_uninst_str
res3: String = No 'self' passed to this method, and no instantiation. It's static!

scala> Automobile.wheels
res4: Int = 4

scala> Automobile.wheels = 5
Automobile.wheels: Int = 5

scala> Automobile.wheels
res5: Int = 5
```

The following section is going to be a *very* light treatment of inheritance in Scala and Python. I recommend reading more on both languages regarding abstract base classes and traits (Scala) and Method Resolution Order (Python). For now, here are the basics.

Scala supports single inheritance via abstract base classes, which are explicitly named as such. Python can treat any class as an abstract one:

##### Python
```python
class Automobile(object):

    wheels = 4
    lights = 2
    doors = 2

    def __init__(self, color, make):
        self.color = color
        self.make = make

    def towing_capacity(self):
        pass

    def top_speed(self):
        pass

    def print_make_color(self):
        print(" ".join([self.color, self.make]))

class Car(Automobile):

    doors = 4

    def __init__(self, color, model):
        super(Car, self).__init__(color, model)

    def towing_capacity(self):
        return 0

    def top_speed(self):
        return 150


>>> mycar = Car("red", "Toyota")
>>> mycar.doors
4
>>> mycar.towing_capacity()
0
>>> mycar.top_speed()
150
>>> mycar.print_make_color()
Red Toyota
```

##### Scala
```scala
abstract class Automobile(val color:String, val make:String) {
    val wheels:Int = 4
    val lights:Int = 2
    val doors:Int = 4

    def towing_capacity: Int
    def top_speed: Int
    def print_make_color():String = return s"$color $make"
}

class Car(color:String, make:String) extends Automobile(color, make) {

    override val doors = 4 // Override needed if immutable "val"

    def towing_capacity() = 0
    def top_speed() = 150
}

scala> val mycar = new Car("Red", "Toyota")
mycar: Car = Car@351cdd99

scala> mycar.print_make_color()
res2: String = Red Toyota

scala> mycar.doors
res3: Int = 4

scala> mycar.top_speed
res4: Int = 150

// Abstract classes only support single inheritance!
scala> abstract class SportPackage {}
defined class SportPackage

scala> class Car(color:String, make:String) extends Automobile(color, make) with SportPackage(){}
<console>:9: error: class SportPackage needs to be a trait to be mixed in
       class Car(color:String, make:String) extends Automobile(color, make) with SportPackage(){}
```

Generally, you should only use abstract base classes in Scala if you need Java interop or need to pass constructor parameters to the base class. Otherwise, you should use what Scala calls "Traits", which act like class mixins and enable multiple inheritance in Scala.

##### Python
```python

class Engine(object):

    started = False

    def start(self):
        self.started = True

    def shutdown(self):
        self.started = False

class Transmission(object):

    fluid_level = 0

    def add_fluid(self, amount):
        self.fluid_level = self.fluid_level + amount

# Using Automobile class from earlier
class Car(Automobile, Engine, Transmission):

    doors = 4

    def __init__(self, color, model):
        super(Car, self).__init__(color, model)

    def towing_capacity(self):
        return 0

    def top_speed(self):
        return 150

>>> mycar = Car("Red", "Toyota")

>>> mycar.start()

>>> mycar.started
True

>>> mycar.fluid_level
0

>>> mycar.add_fluid(50)

>>> mycar.fluid_level
50
```

##### Scala

trait Engine {
    var started:Boolean = false
    // These don't return anything, so no "=" needed
    def start() {started = true}
    def shutdown() {started = false}
}

trait Transmission {
    var fluid_level:Int = 0
    def add_fluid(amount:Int) {fluid_level = fluid_level + amount}
}

class Car(color:String, make:String) extends Automobile(color, make)
  with Engine
  with Transmission {

    override val doors = 4 // Override needed if immutable "val"

    def towing_capacity() = 0
    def top_speed() = 150
}

scala> val mycar = new Car("Red", "Toyota")
mycar: Car = Car@38134991

scala> mycar.start()

scala> mycar.started
res2: Boolean = true

scala> mycar.add_fluid(50)

scala> mycar.fluid_level
res4: Int = 50
```
