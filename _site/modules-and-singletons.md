You may be familiar with the singleton pattern: defining a class intended to
have one, and *only* one, instance. There are various ways to implement
this in Python, but one suggests not defining a class at all, but a module.

Suppose you had a class you want to ensure was instantiated once:

    class Foo:
        x = 3
        def bar(self, y):
            return self.x + y


You could write a script that creates globals for the class and instance data,
and global functions for the methods:

    # foo.py
    x = 3


    def bar(y):
        global x
        return x + y

The primary benefit of this is that you can use `import` as many times as you like to "instantiate" the class

    import foo

but it will only create one instance, the module added to `sys.modules`. All
other inputs will simply return the original instance.

This is fiiine, but a little cumbersome. Suppose you wanted to define a large number of such classes:

    class Element:
        def __init__(self, name, an):
            self.name = name
            self.symbol = symbol
            self.number = an


    class
