# Reproducible environments

## Setup a **reproducible** environment

In the context we are discussing, *setting up the environment* means to make sure
that all the *non-python* programs and libraries that you application needs are available.

So, if your code is calling for example `gdalinfo` or `pdflatex` using `subprocess`,
it is your job to make sure that the program is there.

A crucial detail is that the environment should be **reproducible**.
And this affects both the *development* environment and the *production* environment

[Reproducible dev-environments](https://www.gitpod.io/blog/dev-env-as-code/) mean that in case:

- your laptop breaks down, you can [easily](https://dilbert.com/strip/2017-01-02) continue your work on a different one
- a new developer joins the team, he can start doing actual work without too much trouble
- you stop working on the project, you can easily hand-over to someone else.

Reproducible prod-environments are *essential* for keeping your sanity...

There are multiple ways you can handle the creation of reproducible environments.
I will not cover them in detail here, but reasonable choices are:

- [`docker`](https://www.docker.com/)  which is probably the most flexible, but it also has a relatively steep learning curve.
   Nevertheless, learning at least the basics is really worth it.
- [`ansible`](https://www.ansible.com/) which is useful when you work with VPS.
- [`conda`](https://docs.conda.io/en/latest/miniconda.html) which is the easiest to get started with, but it cannot really help you with

> Note: In production, you often use a combination of the above.
> E.g. you create a VPS, you use `ansible` or [`terraform`](https://www.terraform.io/) in order to set it up, "harden" it and install plain `docker` or [`kubernetes`](https://kubernetes.io/) which is what you actually use to run your code.
