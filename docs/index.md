# Suggestions for Python Development on **Linux**

## tl;dr

The suggested setup is:

0. Linux
1. setup the environment in a reproducible way (e.g. using `docker`, `ansible`, `conda`, etc)
2. Use a modern python version (3.6+)
3. Create a [virtualenv](https://docs.python.org/3/tutorial/venv.html)
4. manage the python dependencies with [poetry](https://python-poetry.org/docs/)
5. \[Ooptional\] install python cli applications using [pipx](https://github.com/pipxproject/pipx)

## Disclaimer

First of all, a couple of definitions:

- A **library** is a provider of an API, i.e. code that gets *imported* by other libraries or applications
- An **application** is a consumer of APIs, i.e. code that *imports* other libraries

The suggestions in this document are written from the point of view of the *application* developer.

The requirements for *library* developers are different (more complex).

> Note: Obviously, the distinction made here is quite high level.
> You can have code that is both a library and an application,
> you can have a library where only part of the APi is public while the rest of the code is not meant to be imported, etc

The reason we make this distinction is that in an *application* you only care for your code to be
running with a specific python version. On the other hand, in a *library* you must e.g. avoid
pinning your requirements to specific versions, test with multiple python versions etc.
