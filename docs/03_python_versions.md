# Python Versions

## Which version of Python should I use?

As of today (June 2020), if you start a *new project*, you should be using Python 3.8.2+

Python 3.7.2+ is OK too.

Versions below 3.6 should be avoided since they lack support for
numerous, backward incompatible, language features including:

- f-strings
- type annotations
- async support
- dataclasses

## When should I upgrade my Python version?

When developing an application, upgrading the python version is not something that you are required to do.
Often, it is perfectly fine to continue using an older version,
especially, for applications that are not being actively developed.

That being said though, if you continue to develop your application
sticking to the older versions comes with certain drawbacks:

1. you are potentially missing security enhancements
2. you are missing new language features
3. the more you postpone upgrading (e.g. if you skip a version or two) the more difficult is going to be to make the upgrade eventually.

Upgrading python versions is something that you can  schedule to do every 18-24 months and,
to the extent that you have a comprehensive test suite, it can be a relatively painless experience.

Using new python releases (i.e. `X.Y.0` and `X.Y.1`) should be avoided since you may encounter various problems (e.g. missing wheel packages etc).
So, wait until at least X.Y.2 comes out.
