# Class Inheritance in Python

So far, we've discussed each new class as if it was totally independent of all other classes. However, classes may exhibit a natural hierarchy with different attributes and methods associated with different levels of the hierarchy. More specific levels of the hierarchy can inherit attributes and methods from higher levels. To make this more concrete, let's think about an example using animals.

First, let's define a generic class for `animal`s:

        class animal:
            """A class to store information about any animal"""

            def __init__(self, group="mammals", endangered=False):
                self.group = group
                self.endangered = endangered

            def summarize(self):
                if (self.endangered):
                    print("This animal is endangered and is a member of the %s." % (self.group))
                else:
                    print("This animal is not endangered and is a member of the %s" % (self.group))

Now, let's think about a specific set of `animal`s that might have different properties - `pet`s:

        class pet(animal):
            """
            A class to store information about animals that are pets.
            The base class is animal.
            """

            def __init__(self, name="", owner="Jane Doe", rabiesShot=True, group="mammals", endangered=False):
                animal.__init__(self,group,endangered)  # Call base class constructor
                self.name = name
                self.owner = owner
                self.rabiesShot = rabiesShot

            def newRabiesShot(self):
                self.rabiesShot = True
                print("%s has now had a rabies shot." % (self.name))

In this case, `pet`s are a specific kind of `animal`. They share all the properties of a generic `animal` with non-`pet`s, but they also have a specific set of properties that are unique to pets (name, owner, and rabies shot status). To see how this works, let's create a new pet.

        fido = pet(name="Fido",owner="Adam Hurm",rabiesShot=False)

Because `fido` is a pet, it automatically inherits the properties (attributes and methods) of the base class `animal`.

        fido.summarize()

But let's say that you want to be able to use one summarize function that includes all the properties of a generic animal as well as a pet. In this case, you can _override_ the summarize method in the _derived_ class - `pets`.

        class pet(animal):
            """
            A class to store information about animals that are pets.
            The base class is animal.
            """

            def __init__(self, name="", owner="Jane Doe", rabiesShot=True):
                animal.__init__(self)  # Call base class constructor
                self.name = name
                self.owner = owner
                self.rabiesShot = rabiesShot

            def summarize(self):
                animal.summarize(self)
                print("This animal is a pet. Its name is %s." % (self.name))

# Try...Except



# Resources
- [Official Python Tutorial - Class Inheritance](https://docs.python.org/3.7/tutorial/classes.html#inheritance)
- [Official Python Tutorial - Errors and Exceptions](https://docs.python.org/3.7/tutorial/errors.html)

