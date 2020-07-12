# Reproducible environments

## What is an environment?

In the context we are discussing, *setting up the environment* means to make sure
that all the *non-python* programs and libraries that your application needs are available.

For example:

- your code is calling a 3rd party program using `subprocess`.

- one of your python dependencies is
  a "[C-extension](https://docs.python.org/3/extending/extending.html)" and there is no
  [wheel](https://www.python.org/dev/peps/pep-0427/) for it. This means that in order to install it
  you must compile it. In a nutshell, both `gcc` and the python headers must be available (you
  install the latter by installing the `python-dev` package on debian/ubuntu).

*Setting up the environment* means to make sure that whatever is required in order to start
developing *is* available.

## **Reproducible** environments

A crucial detail is that the environment should be **reproducible**.  This is something that affects
both the *development* environment and the *production* environment

[Reproducible dev-environments](https://www.gitpod.io/blog/dev-env-as-code/) mean that in case:

- your laptop breaks down, you can [easily](https://dilbert.com/strip/2017-01-02) continue your work on a different one
- a new developer joins the team, he can start doing actual work without too much trouble
- you stop working on the project, you can easily hand-over to someone else.

Reproducible prod-environments are *essential* for keeping your sanity...

## Setting up a **reproducible** environment

To what extends you will go to create reproducible environments depends, among other things, on:

- the complexity of the project
- the importance of the project
- the number of devs that work on it

!!! tip

    For "run-once-and-throw-away" scripts you obviously do nothing.

For really simple projects and projects that only you work on, it is usually enough to just document
any special needs in the readme. I.e. it usually not worth it to setup an automatic way to reproduce
the environment.

For more complex stuff though, there are multiple ways with which you can handle the
"reproducibility" of the environment.  I will not cover them in detail here, but reasonable choices are:

- [`docker`](https://www.docker.com/)  which is probably the most flexible, but it also has a relatively steep learning curve.
   Nevertheless, learning at least the basics is really worth it.

- [`ansible`](https://www.ansible.com/) which is useful when you work with VPS.

- [`conda`](https://docs.conda.io/en/latest/miniconda.html) which, especially among scientists, is
  a popular choice but it IMHV has [several shortcomings](app_conda.md). Among other things, often is not even an
  option for running things on production (e.g. if you run your code on a HPC/HTC cluster conda
  might be forbidden as it can be a security nightmare for the sys-admins).

> Note: In production, you often use a combination of the above.  E.g. you create a VPS, you use
> `ansible` or [`terraform`](https://www.terraform.io/) in order to set it up, "harden" it and
> install plain `docker` or [`kubernetes`](https://kubernetes.io/) which is what you actually use to
> run your code.
