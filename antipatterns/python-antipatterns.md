<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
# Table of Contents

- [Python Antipatterns](#python-antipatterns)
  - [Redundant type checking](#redundant-type-checking)
  - [Restricting version in setup.py dependencies](#restricting-version-in-setuppy-dependencies)
  - [Unwieldy if... else instead of dict](#unwieldy-if-else-instead-of-dict)
  - [Overreliance on kwargs](#overreliance-on-kwargs)
  - [Overreliance on list/dict comprehensions](#overreliance-on-listdict-comprehensions)
  - [Mutable default arguments](#mutable-default-arguments)
  - [Using `is` to compare objects](#using-is-to-compare-objects)
  - [Instantiating exception with a dict](#instantiating-exception-with-a-dict)
  - [Not strictly pinning all packages](#not-strictly-pinning-all-packages)
- [Reference](#reference)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Python Antipatterns
===================

Redundant type checking
-----------------------

Bad:

```python
def toast(bread):
    if bread is None:
        raise TypeError('Need bread to toast.')
    if bread.is_toastable:
        toaster.toast(bread)
```

In this case, checking against `None` is totally useless because in the next
line, `bread.is_toastable` would raise `AttributeError: 'NoneType' object has
no attribute 'is_toastable'`. This is not a general rule, but in this case
I would definitely argue that adding the type checks hurts readability and adds
very little value to the function.

Good:

```python
def toast(bread):
    if bread.is_toastable:
        toaster.toast(bread)
```

Restricting version in setup.py dependencies
--------------------------------------------

Read those articles first:

* [setup.py vs.
  requirements.txt](https://caremad.io/2013/07/setup-vs-requirement/)
* [Pin Your Packages](http://nvie.com/posts/pin-your-packages/)
* [Better Package Management](http://nvie.com/posts/better-package-management/)

**Summary: The main point is that `setup.py` should not specify explicit version
requirements (good: `flask`, bad: `flask==1.1.1`).**

In a few words, if library `lib1` requires `flask==1.1.1` and library `lib2`
requires `flask==1.1.2`, then you'll have a conflict and won't be able to use
them both in application `app`.

Yet in 99.999% of the cases, you don't need a specific version of flask, so:

* `lib1` should just require `flask` in `setup.py` (no version specified, not
  even with inequality operators: `flask<=2` is bad for instance)
* `lib2` should just require `flask` in `setup.py` (same)

`app` will be happy using `lib1` and `lib2` with whatever version of `flask` it
wants.

`app`'s `requirements.txt` should be as specific as possible, ideally
strictly pinning (`==`) every single dependency. This way the app's stability
will be very predictable, because always the same packages version will be
installed.

Usually apps only use `requirements.txt`, not `setup.py`, because `pip install
-r requirements.txt` is used when deploying.

The only exception for pinning a dependency in a library is in case of a known
incompatibility, but again this should be a very temporary move, because that
will prevent people from upgrading.

Ruby has a pretty similar dichotomy with [Gemspec and
gemfile](http://yehudakatz.com/2010/12/16/clarifying-the-roles-of-the-gemspec-and-gemfile/).

Unwieldy if... else instead of dict
-----------------------------------

Bad:

```python
import operator as op


def get_operator(value):
    """Return operator function based on string.

    e.g. ``get_operator('+')`` returns a function which takes two arguments
    and return the sum of them.
    """
    if value == '+':
        return op.add
    elif value == '-':
        return op.sub
    elif value == '*':
        return op.mul
    elif value == '/':
        return op.div
    else:
        raise ValueError('Unknown operator %s' % value)
```

Note: the operator module is a standard library modules that defines base
operator functions. For instance `operator.add(1, 1) == 2`.

This huge switch-like expression will soon become really difficult to read and
maintain. A more pythonic way is to use a dict to store the mapping.

Another reason is that to get 100% line and branch coverage, you will have to
create as many tests as you have mappings. Yet you could consider that the
value to operator mapping is part of the codebase's configuration, not its
behavior, and thus shouldn't be tested.

Good:

```python
import operator as op

OPERATORS = {
    '+': op.add,
    '-': op.sub,
    '*': op.mul,
    '/': op.div,
}


def get_operator(value):
    """Return operator function based on string."""
    operator = OPERATORS.get(value)
    if operator:
        return operator
    else:
        raise ValueError('Unknown operator %s' % value)
```

Overreliance on kwargs
----------------------

TODO

Overreliance on list/dict comprehensions
----------------------------------------

TODO

Mutable default arguments
-------------------------

TODO

Using `is` to compare objects
-----------------------------

TODO

[Why you should almost never use “is” in
Python](http://blog.lerner.co.il/why-you-should-almost-never-use-is-in-python/)

Instantiating exception with a dict
-----------------------------------

Example:

```python
def main():
    raise Exception({'msg': 'This is not a toaster', 'level': 'error'})
```

Why is this an antipattern? Exception are meant to be read by human beings.
Thus, their first argument should be a human-readable error message, like this:

```python
class NotAToasterException(Exception):
    pass


def main():
    raise NotAToasterException('This is not a toaster')
```

Most tools expect this, most importantly
[Sentry](https://getsentry.com/welcome/) which is a tool used to get alerts
when exception are raised in production. An `Exception`'s message should be
short so that it can be displayed on a single line.

If you need to attach custom metadata to an exception, the proper way is to
have a custom constructor:

```python
class NotAToasterException(Exception):

    def __init__(self, message, level):
        super(NotAToasterException, self).__init__(message)
        self.message = message
        self.level = level


def main():
    raise NotAToasterException('This is not a toaster', 'error')
```

## Not strictly pinning all packages

Example of bad `requirements.txt` file:

```
sqlalchemy
flask
```

Another example of a bad `requirements.txt` file:

```
sqlalchemy>=0.9
flask>0.10
```

Good:

```
Flask==0.10.1
Jinja2==2.8
MarkupSafe==0.23
SQLAlchemy==1.0.12
Werkzeug==0.11.4
itsdangerous==0.24
```

This ensures that there's absolutely no ambiguity as to which package will be installed on production. If you forget to mention even a single package, you will perhaps have a different version on your testing/dev environment, and in your production environment.

The proper way to update a package and its dependency is to use another tool, for instance [pip-tools](https://github.com/nvie/pip-tools). If you have multiple applications and you want to mass update a package, then you'll have to write a script to do so. Keep things simple and explicit, then use scripts on top of it to instrument your processes.

**Reference**

* [Pin Your Packages](http://nvie.com/posts/pin-your-packages/)

# Reference

* [Pythonic Pitfalls](http://nafiulis.me/potential-pythonic-pitfalls.html)
* [Python Patterns](https://github.com/faif/python-patterns)
* [The Little Book of Python
  Anti-Patterns](http://docs.quantifiedcode.com/python-anti-patterns/)
* [How to make mistakes in
  Python](http://www.oreilly.com/programming/free/files/how-to-make-mistakes-in-python.pdf)
G
