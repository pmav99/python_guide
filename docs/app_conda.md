## What `conda` really is

Half the posts you will find online compare `conda` to `pip`.  IMHV this is really unfortunate.
`conda` is not really comparable to `pip`.

`pip` **only** deals with *python* packages that are available through a [Python
Package Index](https://pypi.org/).

`conda` on the other hand, is a **generic package manager**.  A more likely comparison is to compare
it with `apt` or `yum`.  `conda` can install **compiled binaries**.  E.g. you can use conda to
install `gcc`, or `openssh-client`


With `conda` you can create a *parallel* installation of the OS (not of the kernel, but of the
userspace).  It practically allows you to have parallel "branches"  where you can install different
versions of programs and libraries, and it gives you an easy way to switch between them.

!!! Tip

    This is a similar concept to python's virtualenvs but `conda` has a much bigger scope.

So you can have one branch/environment where you install for example GDAL version 2 and another
where you install GDAL version 3.  Creating a similar setup without `conda`, is doable of course,
but before docker became a thing, it was a pain.

!!! Warning

    Security-wise this is a nightmare though. `conda` gives you a *really* easy way to bypass root
    permissions...

## Why not `conda`

Personally, since I almost exclusively deal with Linux, I don't find much benefit in `conda`.

- it is [notoriously](https://github.com/QuantStack/mamba) slow,
- it takes a huge amount of space,
- downloading random binaries from the internet is rather iffy from a security point of view,
- conda binaries are usually compiled with generic options so performance can be sub-optimal,
- etc, etc.

All in all, IMHV `docker` + `apt` + `pip` is more than an adequate alternative, and I would even
say, a superior alternative.

!!! note

    Of course `docker` has a learning curve, and I am talking here from the point of view of someone
    who has already paid the price, so you could say that I am biased...

## When `conda` really shines?

IMHV `conda` makes a lot of sense on OSes that make it really difficult to compile things from
source (i.e. Windows). In these environments installing a Python C-Extension to can be a real PITA.

It also makes some sense on e.g. Mac OS if you want to avoid using homebrew etc. Installing binaries
is easier after all.

On Linux though you don't really have such problems.  Even if you need to compile something, it is
usually relatively easy to do so (or at the very least, easier than the other OSes).

## How can you use `conda` on linux?

If you decide to use `conda` you should use it *to setup your* **environment**. For a more detailed
explanation of what this entails, please check the [relevant
section](02_reproducible_environment.md).  In a nutshell, in the context we are discussing, it means
to make sure that all the packages and libraries that you application needs are available.

To make this clear, it might make sense to include in the discussion `pip`.

`pip` is a package manager. Nevertheless, it **only** deals with Python packages.  You can't install
non-python stuff with `pip`.  So for example you can't install `gcc` or `gdalinfo` with `pip`.  You
can only install the [python bindings for GDAL](https://pypi.org/project/GDAL/), not
[GDAL](https://gdal.org/) proper.

So, if your code is calling another program using e.g. `subprocess`, it is your job to make sure
that the program is there. `pip` can't help you with that.

That's where `conda` comes in.

So you should use conda to:

- create your *environment*,

- install the non-python dependencies there (e.g. `python=3.7.3`, `gdal=3.0.4` etc). These
  dependencies should be pinned in your `environment.yaml`.

- and then create a virtualenv using the python you installed via `conda`

- and manage your python dependencies using `poetry`. These dependencies should be pined in your
  `pyproject.toml/poetry.lock`

This way, you can continue to use the standard python ecosystem and have consistency across
different environments and OSes.

!!! Tip

    If you do decide to use `conda` though, my suggestion is to use `conda` all the way.  So if you
    need e.g. `GDAL` and `openssl` install both from `conda`, not one with `conda` and the other
    with `apt`.

!!! Warning

    REMEMBER: don't mix up packages from different package managers in your environment. This can
    only lead to trouble.

