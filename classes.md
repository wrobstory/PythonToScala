Classes

Building classes with Scala is simpler than Java (woo!), but still with some added intricacies that you won't usually see when building Python classes. It's probably best just to compare a class that behaves the same for the two languages: 

Python:
```python 

class Plane(object): 

    _crew = 0
    passengers = 0

    @property
    def crew(self):
        pass

    @crew.setter
    def crew(self, crew):
        if crew < 0:
            raise ValueError("Crew cannot be less than 0!")
        else:
            self._crew = crew

    @crew.getter
    def crew(self):
        return self._crew

    def board(self):
        self.passengers += 1

    def count_passengers(self):
        return self.passengers
```