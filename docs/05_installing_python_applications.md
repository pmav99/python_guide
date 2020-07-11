# Installing Python **applications**?

While developing you will very often need to make use of some python CLI application.
Nevertheless, often these applications are not packaged for your distribution and/or
if you use a server distro or an LTS distro, the packages might be ancient.

Prime examples of such applications are:

- [ansible](https://pypi.org/project/ansible/)
- [docker-compose](https://pypi.org/project/docker-compose/)
- [pgcli](https://www.pgcli.com/)
- [poetry](https://python-poetry.org/)
- [invoke](https://www.pyinvoke.org/)
- [httpie](https://httpie.org/)

There are multiple ways that you can install such applications.
For good or for bad, not all of them are equal.

## What not to do?

Unfortunately, some quite popular suggestion from the internet should be **avoided**:

1. `sudo pip install`
1. `pip install --user`
1. `apt install`, `yum install` or any other distribution pacakge manager

### What is the problem with `sudo pip install`

You should **NEVER** use `sudo pip install`.
Unless you want to end up with a broken linux installation, that is.

The problems is that by using `sudo pip install` you may override/replace files that were previously installed by `apt`.
Moreover, you might upgrade some packages to versions that are not compatible
with other packages that are currently installed.
And don't forget that the Python is being used by the linux distribution itself.

So whenever you run `sudo pip install` you run the risk of breaking your Linux distribution
in ways that might not be apparent and which might bite you even years later!
And the worst is that you will break something and you will have zero warning that you did break it.

For example if you try to upgrade ubuntu 18.04 to 20.04 the upgrade might fail because
the files you have under `/usr` are no longer managed by `apt`, because you updated a package with `sudo pip install`

Recovering the system from `sudo pip install` is possible but it is not fun and you must know what you are doing.

### What is the problem with `pip install --user`

`pip install --user` installs packages in `~/.local/lib/pythonX.Y/site-packages`

The problem is that `pip` does not do dependency resolution
(in the future this [is planned to change](https://github.com/pypa/pip/issues/988)).
It just installs packages. For example:

- package A requires package K Version <2.0
- package B requires package K Version >2.0

If you do `pip install --user A` you will also install `K` version 1.X.
If you follow this command with `pip install --user B`,
then `K` will be upgraded to version 2.X and `A`
will be broken **without any warnings**.

So, by using `pip install --user` you solve a short term problem but you might introduce other problems in the future that might be hard to debug.

And  anyhow, since there are way cleaner options, why use something suboptimal?

### How about installing stuff with my distro's package manager (e.g. `apt` or `yum`)?

The package manager can work just fine as long as you stick it.
There are some  downsides though:

- not everything is available
- packages are often outdated
- most often than not you are forced to use a specific version

As an application developper,  I want to have the freedom to solve the problem I am facing in the best way possible.
Fighting with old APIs is not helping in that direction.

### How about creating a virtualenv and installing the application there?

This is by far the best option.
You achieve complete isolation of the application both from other applications and from the system.
Nevertheless, it is cumbersome:

- You need to create the virtual environment manually
- install the package manually
- create symlinks to `~/.local/bin` manually
- you need to remember to remove the symlinks when you remove the application.

Thankfully, there is a tool that automates the virtualenv procedure. It is called [pipx](https://github.com/pipxproject/pipx).

### `pipx`?

[`pipx`](https://pipxproject.github.io/pipx/) is a package that lets you Install and Run Python Applications in Isolated Environments.

#### Installation

`pipx` only has two requirements:

1. Python 3.6+
2. `~/.local/bin` must be in your `$PATH`

To install it you should use:

```
python3 -mpip install --user pipx
```

yes, earlier, we suggested **not** to use `pip install --user`, but
we will only be installing this very package with `pip install --user`.
All the others will be installed by `pipx` itself.

### Usage

Using pipx is pretty simple. you just run

```
pipx install <package-name>
```

where `<package-name>` is the name of any PyPi package.
Behind the scenes, `pipx` will:

1. Create a dedicated Virtual Environemnt in `~/.local/pipx/virtualenvs`
2. Install the application in the virtualenv
3. Create a symlink from `~/.local/pipx/virtualenvs/<package_name>/bin/<executable>` to `~/.local/bin`

To uninstall a package you just:

```
pipx uninstall <package_name>
```

and this will remove both the virtualenv and the symlink
