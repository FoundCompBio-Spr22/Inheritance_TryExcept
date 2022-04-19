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



# Try...Except
