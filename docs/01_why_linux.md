The choice of the operating system is for sure a controversial topic.  Among other things it is
a question of aeshetics, specific needs and it often boils down just to personal preference.

Nevertheless, I am arguing that when it comes to Python there usually is enough justification to
choose Linux over other OSes.

!!! note

    For sure, any modern operating system **can** server your needs. The question what is the **best**
    way to serve your (programming) needs.

!!! tip

    In this guide I am only describing what works for me. You should choose the OS that is serving
    **your** needs in the best possible way.

## `dev` vs `prod`

An important distinction is between:

- the development environment (i.e. where you *write* the code)
- the production environment (i.e. where you *run* the code)

In order to make debugging easier, you should strive to make the development environment as similar
as possible to the production environment.

## Why Linux?

As far as I am concerned, I consider myself I professional. When it comes to my work I want to be
using the best tools I can, no questions asked.

Just to give you a few examples:

- There is a great deal of unix tools that make development so much easier
  and which are not available on Windows. Some of them are available on Mac OS, but not all; see
  the next point.

- Not having **native** docker is a huge deal breaker for me. It is not that it doesn't work on
  other operating systems, but as soon as you move on from simple cases you will eventually
  encounter a bug or some incompatibility and you will have to start jumping through hoops.

- Practically speaking, in science and web-development,
  the vast majority of the code that you will write will be executed on Linux (HPC, HTC,
  super-computers, web servers etc). Remember what we said about minimizing the differences between
  `dev` and `prod`?

- There is some truth in (big) numbers. [1 in 4 developers use
  Linux](https://insights.stackoverflow.com/survey/2020#technology-developers-primary-operating-systems)
  (regardless of Programming Language). When it comes to developers that identify themselves as
  primarily Python devs, [70% of them use
  Linux](https://www.jetbrains.com/lp/python-developers-survey-2019/#DevelopmentTools) at some
  capacity (main OS or cnotainers).

!!! note

    Is the Linux world a fairy-tale? Nope! E.g. when it comes to multimedia it **is** a *living
    hell*. But here we are talking about development. Not about watching movies, using bluetooth
    devices etc.

## Why not Mac?

It is unix based. It is very polished when it comes to integration with the
native applications.  Many devs like Mac OS. Nevertheless, it is *like* Linux. It is *not* Linux.

!!! note

    I spend most of my working time in front of a console and linux is better at that.

## Why not windows?

In the past, Python on Widows was really a second class citizen. Nowadays, with platforms like
[conda](app_conda.md) the situation is for sure better, nevertheless there are still restrictions.
For example:

- Eventually you will need something that is not available via a pre-compiled package and compiling
C-Extentions on Windows is a major PITA.

- Dealing with multi-processing and multi-threading on windows is not what you call fun.

- There are a lot of subtle details that are different than Linux and usually that's where you will
  run your code.

## How about VMs and WSL?

There are two more options:

- Using Windows or Mac as the host operating system and using Linux in a Virtual Machine (VM)
- Using Windows Subsystem for Linux (WSL)

For a short period, I did use a VM and
[someone](https://www.youtube.com/channel/UC46xhU1EH7aywEgvA9syS3w) whose opinion I value [uses it
extensively](https://www.youtube.com/watch?v=8KdAqlESQJo). In the past (2000s) when computers were
much weaker it was not really a viable choice.  Nowadays, it works just fine though.

Personally I haven't used WSL. I know that it is being actively developed/improved. It is for sure
a technology worth keeping our eyes upon.

As of today, between the two, I think I would choose a VM.
