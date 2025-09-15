# Classes

- `__init__()` method is a special method that Python runs automatically whenever we create a new instance based on the Dog class.
- The `self` parameter is required in the method definition, and it must come first, before the other parameters.

```python
class Dog:
    """A simple attempt to model a dog."""
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def update_age(self, age):
        self.age = age
    def sit(self):
        print(f"{self.name.title()} is sitting.")

my_dog = Dog('harry', 4)
print(my_dog.name)
my_dog.sit()
my_dog.update_age(10)
print(my_dog.age)
```

## Inheritance

The `super()` function is a special function that allows you to call a
method from the parent class.

```python
class Car:
    def __init__(self, make, model, year):
        """A simple attempt to represent a car."""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        long_name = f"{self.year} {self.make} {self.model}"
        print(long_name.title())

class ElectircCar(Car):
    def __init__(self, make, model, year):
        super().__init__(make, model, year)
        self.battery_size = 40

    # define attributes and methods for the cuild class
    def describe_battery(self):
        print(f"Battery size: {self.battery_size}")

my_tesla = ElectircCar('tesla', 'model x', 2023)
my_tesla.get_descriptive_name()
my_tesla.describe_battery()
```

### Overriding Methods From the Parent Class

```python
class Car:
    # ...
    def fill_gas(self, gas):
        self.gas = gas

class EletricCar(Car):
    def fill_gas(self):
        print('this car does not have gas tank')
```

### Instance as Attributes

You can break your large class into smaller classes that work together, this approach is called **composition**.

```python
class Car:
    # ...

class Battery:
    def __init__(self, battery_size=40):
        self.battery_size = battery_size

    def discribe_battery():
        print(f"Battery size is {self.battery_size}")

class ElectircCar(Car):
    def __init__(self, make, model, year):
        super().__init__(make, model, year)
        # composition here!!
        self.battery = Battery()

my_tesla = ElectircCar('tesla', 'model x', 2023)
my_tesla.battery.describe_battery()
```
