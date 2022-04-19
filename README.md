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

When Python code trys to do something that's invalid, it will raise an error. Some errors are due to improper syntax that Python simply can't interpret. These syntax errors need to be corrected before the code can be executed.

However, other errors occur at runtime, and are known as Exceptions. These aren't due to improper syntax, but rather due to attempts to do things that simply don't make sense (for example, performing a mathematic operation with a string).

By default, Python stops execution when Exceptions are raised and trys to print out an informative error message (listing the type of Exception and the lines it tried to execute when the problem occurred). However, you the programmer can dictate what happens when different types of Exceptions are raised.

To dictate how a program handles exceptions, you will need to use `try` and `except` statements. Code inside the `try` will be monitored for any Exceptions that could occur. If one does occur, then execution immediately shifts to the code in the `except` block. If no Exception is raised, then the `except` block is never executed.

        try:
            filename = "input.txt"
            inputFile = open(filename,'r')
        except OSError:
            print("There is no file called %s." % (filename))

Code in `except` blocks allow you to handle expected problems in an organized way, often providing the user (or you) with an informative message that lets them know what they should do next.

Ideally, `except` blocks should only catch those exceptions that are expected (in this case, an `OSError`). If you don't specify an exception type, they will catch all exceptions (even ones you may not have anticipated) and lead to unexpected behavior or non-sensical error messages. To illustrate this difference, compare what happens with this code block:

        try:
            filename = "input.txt"
            1/0
            inputFile = open(filename,'r')
        except OSError:
            print("There is no file called %s." % (filename))

...and this one...

        try:
            filename = "input.txt"
            1/0
            inputFile = open(filename,'r')
        except:
            print("There is no file called %s." % (filename))


        What happened in the 2nd case? Is this desirable?

`try...except` blocks can also be followed by an `else` statement. In this case, the `else` statement is executed if no exception is raised in the `try` block. So, this is code that is alternative to that in the `except` block.

You can also customize exceptions in a couple of different ways. First, you can raise an exception whenever you want. In other words, you can build tests into your code, and flag problems when those tests aren't satisifed.

        try:
            myWord = input("Enter a word with five letters: ")
            assert len(myWord) == 5
        except AssertionError:
            print("You didn't enter a word with five letters!")

What's this `assert` thing? It's basically doing the same thing as this.

        try:
            myWord = input("Enter a word with five letters: ")
            if (len(myWord) != 5):
                raise ValueError
        except ValueError:
            print("You didn't enter a word with five letters!")

But let's say you wanted the user to have the opportunity to keep entering words until they provided one that met your criterion.

        while True:
            try:
                myWord = input("Enter a word with five letters: ")
                assert len(myWord) == 5
                break
            except AssertionError:
                print("You didn't enter a word with five letters!")

Let's unpack this. What's going on here?

You can also define your own types of exceptions.

        class wordLengthError(Exception):
            """
            Exception raised when word is not the right length.
            """

            def __init__(self,message):
                self.message = message

        try:
            myWord = input("Enter a word with five letters: ")
            if (len(myWord) != 5):
                raise wordLengthError("Word not five letters!")
        except wordLengthError:
            print(wordLengthError.message)

# Resources
- [Official Python Tutorial - Class Inheritance](https://docs.python.org/3.7/tutorial/classes.html#inheritance)
- [Official Python Tutorial - Errors and Exceptions](https://docs.python.org/3.7/tutorial/errors.html)

