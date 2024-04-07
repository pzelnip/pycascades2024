# Pycascades 2024

<https://2024.pycascades.com>

## Types, In My Python?!

Piper Thunstrom

<https://pretalx.com/pycascades-2024/talk/HLAM8G/>

<https://piper.thunstrom.dev>

> It's more likely than you think!

> Types, In My Python? is an analysis of Python's unique relationship to typing systems.
>
> I will start by examining Python's strange dual nature:
> A dynamically typed scripting language that more or less works as expected.
> A strongly typed language with strict limits on what you can do with an object,
> and now able to statically analyze your usages to make sure you're doing things right.
>
> Following that, I will examine some of the concepts we talk about as a community in more detail.
> What do we mean by "duck typing", and how does it apply in light of Python's dual nature?
> Why is it static analysis, and not static typing?
>
> To end, I will make a proposal regarding the best method to use both sides of Python's type > system.
> The goal is to accelerate your development and reduce tedium.
> Is there a happy middle ground between strict static typing and a dynamic free-for-all?

Discussion of dynamic vs strong typing

Rust as ex of strong typing

Two categories:

* strongly vs weakly typed
* Dynamically typed vs statically typed

Both are spectrums

Python is a dynamic language thats failly strongly typed

(ex: string + int == error)

### Principles of Python's Type System

Duck typing

Protocols, other words: Interface or Contract

Josh Cannon at Northbay Python: youtube link CSpzTxS8B0

Type Hinting

* support satic analysis of your python code
* Makes tools work better
* Provides us the Protocol type for declarative structural typing

static analysis is not static typing (optionality)

### Applying the Theory

Python is strongly typed (uses runtime system to enfroce correctness), Python likes protocols)

"The more specific the type hyint, the better the tools can do their jobs"

Tips:

* make your return types a s concrete as possible (ex `list[str]` vs `list`)
* declarative data tyeps
  * Dataclasses
  * NamedTuple
  * TypedDict
* other useful tools
  * typing.Union (or type1 | type2)
  * typing.Optional (or type1 | None)
* Parameters
  * You want the leas t specific type your code can handle
  * Use standard library protocols
    * Mapping
    * Sequience
    * Iterable
  * Previously mentioned tools
    * TypedDict
    * Unions
  * Worst case, use Protocol to define exactly what shape your data needs to be

(discussion of typevars & generics)

"Good type hinting is like good testing" -- interesting analogy

Do your best while writing, reap the benefits of this later

---

## The Stories Of the Most Infamous Bugs

Ian Zelikman

<https://pretalx.com/pycascades-2024/talk/RHGEQZ/>

> Whenever we write code we eventually make mistakes and have “bugs”. We employ
> many techniques including testing and reviews to avoid them but some mistakes
> still make it into production. But what are the most famous "bugs"? How they
> happened and is there something common we can learn from them?

@izcoder

### Motivation

Can benefit from learning from past mistakes

### What is a Bug

Wikipedia defn

Some discussion of history of the term "bug" or "buggy", goes back farther
than the Grace Hopper physical bug in a mainframe

### Infamous Bugs

#### Mars Climate Orbiter

1998, collect info about past mars climate, etc

Lost contact after 9 months

Use of metric unit in thrusters vs imperical units used by Nasa

$320M dollar loss

L/M got spec from Nasa, but they didn't follow the spec. But Nasa
Ack'd & put blame on internal testing procedures that should have
found the errro much sooner

Bug ticket was filed early, but not proioritized correctly

#### Ariane 5 Explosion

1996, 1st launche of the rocket, carrying 4 sattelites

Guidiances system had overflow bug

$370M loss, between rocket & sattelites

Software package used reliably in one system, reused in a different context,
and in this case it broke.

Backup system should have kicked in, but in this case backup system
suffered from same issue

#### AAT&T Long Distance Calls

1990, had outage lasting 9 hours

Substantial PR damange to company, $60M lost revenue, $70M from calls not placed

#### Patriot System Failure

Patriot missles

1990's, 1991, in Saudi Aribia in US Air Force base

Iraqi missle fired to base, patriot missle failed to intercept (at Dahhran)

Long running system, internal clock, precision error had overflow

This was accounted for, but only applied in one of the two places it needed to be

28 people dead, 110 injured, mostly reserve duty personel

8 hour for resetart, system was running for 100 hours

#### World End 1983

Sep 26, 1983, russian detected false alarm of missles coming from US

Value of Human Intervention & supervision/coherence check

---

## Intro to Introspection

Jeremiah Paige

<https://pretalx.com/pycascades-2024/talk/HEZUCW/>

<http://slides.ucodery.com/intro-to-introspection>


>Python holds no secrets about your code; except perhaps how to access that information. in this talk you'll find out how to discover almost any information about running python code.
>
>    Introduction (2 minutes)
>        techniques work equally in normal execution, interactive mode, or when debugging.
>        start with the obvious tools like print() before going deeper
>    Name discovery (5 minutes)
>        discover names that will resolve in the current scope
>        discover attributes on a random object
>    Description discovery (5 minutes)
>        how does this object choose to represent itself
>        get back author notes at runtime
>    Type discovery (5 minutes)
>        what is this thing
>        how does this thing relate to other object
>    Code discovery (5 minutes)
>        start using the inspect module
>        lookup signature of callables
>        find exact location in py file object was defined
>    Conclusion (2 minutes)
        >typically, all information available while reading code i also available when running the code
>        don't be afraid to peek inside python
>
Examine running code without source available

Use of `locals()` & `globals()`

Use of some of the various tools in a REPL like `type`, ``callable` etc

Dig into deeper with the `inspect` module

`signature` is neat

INtrospection axioms

* names resolve inner to outer most scope
* everything is an object
* atrribute lookup is based on heritance

Scope Resolution

Names resolve in LEGB order:

* Local
* Enclosing
* Global
* Builtin

Is there a builtin to query Enclosing?

Run through of how the inspect module works

---

## Rest Easy with Jupyrest: Deploy notebooks as web services

Koushik Krishnan

> Jupyter notebooks are awesome! However, a notebook on its own is not a product
> or a service. Bridging this gap usually involves a complete rewrite into a web
> service that leaves behind all the awesome-ness of the notebook. What if we
> didn't have to do this? That's where Jupyrest comes in! Jupyrest is a library
> I created to solve this exact problem for my team at Microsoft. In this talk
> I'll show you how you can turn your Jupyter notebooks into a web service
> without any modifications to it. Jupyrest is being used at Microsoft by data
> scientists to deploy hundreds of microservices.

Serverless in a nutshell

* deploy my code "as is"
* Autmoatic:
  * scaling
  * auth
  * monitoring

Jupyrest

* Deply jupyter notbooks as serverless "notebook functions"
* define in/out contracts for notebooks
* Deved at MS in production since 2020

"Notebook Functions"

* id
* input schema
* output schema

<https://github.com/microsoft/jupyrest>

---

## Oh the (Methods) You Can (Make): By Dunder Seuss

Joshua Cannon

> You can make many methods
> Over 100 to be exact
> That start with two underscores
> What do you think of that?
>
> The runtime, it calls these
> At points A or B
> To do special magic
> At runtime, you see.
>
> You may have seen __getattr__ or __init__
> But __rfloordiv__? What’s the point of it?

Storytime at Pycascades

*Super entertaining talk*.

---

## Embracing MLOps: Bridging the Gap Between Machine Learning and DevOps

Mayank Jindal

> In the dynamic field of machine learning, MLOps (Machine Learning Operations)
> has emerged as a crucial discipline combining aspects of machine learning,
> data science and operations. This talk aims to demystify MLOps differentiating
> it from traditional DevOps practices and highlighting its growing importance.

(virtual talk)

Machine Learning definition

MLOps

* Machine learning operations
* Set of practices to to build deploy & maintain machine learning models

Why MLops

* Speed to deployment
* Operational efficience
* Enahance collaboration
* scalability
* governance

MLOps vs DevOps

* model vs code
* continuous training
* data dependency
* monitoring & performance

Model versioning

*tracking and managing changes to models over time

---

## Pythonic Play: Crafting Interactive Worlds with Python in Game Development

Drishti Jain

> Embark on a thrilling journey into the realm of game development where the
> elegance of Python meets the excitement of interactive experiences! In this
> talk, I will unravel the captivating world of Python game development,
> exploring the tools, techniques, and creative possibilities that make Python a
> formidable language for crafting immersive games.

@drishtijjain

<https://linktr.ee/drishtijjain>

### Game Development

* Collision Detection
* Rendering
* Game loops
* physics

Worked through example of building a snake clone (caterpillar) using turtle & tk

Quick overview libraries for game dev (Pygame, Panda3D, Arcade, Pyglet, Godot Engine),
and some pros/cons

Deeper dive on PyGame

---

## The Best Language to Write Python In Is Rust

Trent Hauck

> Python is an excellent language, in part because of how accessible it is. This
> accessibility means that professionals in finance, science, marketing, etc,
> often can make use of it for their goals. This also means that for programmers
> who write tools for these users, Rust can make an excellent language to
> deliver a fast, stable experience. In this talk we'll discuss more about why
> you might consider augmenting your Python code with Rust and walk through a
> case study for how to achieve it.

<https://twitter.com/trent_hauck>

Lots of Python libraries have Rust under the hood.

* Polars
* Pydantic
* Ruff

Why use Rust with Python?

* Performance
* Ease of implentations
* Ease of distribution

"It might take you a while to get up to speed with Rust.  It's an unforgiving language."

Example of taking a function in Rust to Python package

"traits" like "interfaces", ex: arguments to functions must implemnent `FromPyObject`
Return type must implement `IntoPyObject`

`PyResult` is a `Result` type for PyO3

`maturin` tool for building the module & installing into the current Python environment.

Discussion of how to add things like:

* function signature
* docstrings
* type annotations

Example of a Python class:

* struct
* pymethods

SDLC - we wronte some rust code, how do we shuip it?

* maturin
* Maturin tutorial: <https://www.maturin.rs/tutorial>

Can generate a CI workflow (ex a Github actions workflow)

Special Topic: Data Engineering

* Combination of Rust + Python is really good for data intensive tasks
* Arrow as an Intermideiate, can pass data between Rust & Python without copying
* pyarrow (Python arrow package)

---

## Next Level Python Applications with PyScript

Fabio Pliger

> Zero Installation, massive scalability, mobile support and more. This talk is
> going to cover the super powers of running Python in the Browser and how to
> best use PyScript.

(virtual talk)

@b_smoke

<https://fpliger.pyscriptapps.com/talks-pycascades-2024/latest/>

Creator of Pyscript

JS VS PS: Not a replacement for Javascript, more of an augmentation/complimentary thing

Platform to run Python in the browser

It's a platform

FFI - foreign function interface

Focus on "HUMAN" APIs

<https://pyscript.net>

Showed a ton of cool examples of apps & frameworks built using the library

---

## I declare an environment! - Reproducibility with and _without_ Docker

Sarah Kaiser

> A software project being called "reproducible" can mean a lot of things, but
> usually includes a description of how and where the code in your project can
> be run. Often this means including Python virtual environment, a Conda
> environment, or even a Docker container to help others replicate your work. In
> this talk I will introduce some of the most common ways the scientific Python
> community approaches reproducibility, and what are the advantages and
> disadvantages of the approaches. I will also share a new way that you can make
> not only your Python code but your development machine reproducible without
> Docker containers with a tool called Nix. I will also show an example of using
> a Nix defined operating system (NixOS) with Docker containers to run my home
> lab.

<https://github.com/crazy4pi314/pycascades-repro-envs>

1. Good reproducible envs need declarative and imperative specs
2. A combination of Docker & Nix can make reproducible Python projects easier


Reproducible

* for who?
* on what device?
* when?
* with what resources?

Environments

* Declarative: describe the desired final state as comletely as possible
* Imprerative: provide a list of steps or actions

]![](https://cdn.zappy.app/24a839f728d3445caed5f7ae7bd46cbc.png)

<https://nix.dev/>

<https://nixos.org/>

---

##  Kandinsky: Using KMeans (and friends) to play with the colors of photograph(s)

Shaurya Agarwal

> Clustering is tricky yet absolutely essential for many a Machine Learning
> initiative. The what, the how and the why confound each time we look at the
> data, whether it is customer segmentation (or cohort) analysis or it is
> finding centers of influence or breaking down a population into groups to
> build different models for each.
>
> Studying clustering algorithms like KMeans using toy datasets is insufficient
> (and often tedious) because it does not let you experience real-world
> problems. For e.g. the problem when the centroids don't settle, or situations
> where we have too many or too few clusters. Which distance measure to use and
> when? How to prepare (normalize? standardize?) the dataset for clustering?
>
> Also, not too many real-world scenarios are "visual", unless we plot a graph
> or two, and that fails when we deal with higher dimensions.
>
> What if we could use a non-trivial but visual data source? Like the colors and
> pixels of a photograph, where we could see the data that went in and the
> resultant output clusters? The obvious takeaways of this talk, in my
> experience, are that Data Science and Data Engineering practitioners gain a
> deeper understanding of what's going on in the clustering algorithms in a fun,
> very "visual" and engaging manner; and also build a better intuition about the
> best approach to take for solving a problem.

(virtual talk)

Kandinsky <https://github.com/shauryashaurya/kandinsky>

---

## Day 2

## Lightning Talks

### Mapping Tomorrows Eclipse path with geopandas and pyscript

Christy Heaton

<mas.to/@christyheaton>
]
<https://pyscript.com/@cheaton/2024-eclipse>

### How to do the same thing over and over again

@JessicaGarson

Snr dev advocate at Elastic

script for updating data -> google cloud function -> Google Cloud scheduler to update index

<https://github.com/JessicaGarson/>

### Beautiful Reporting With Quarto

Sam Edwardes (dude we had lunch with)

<https://quarto.org/>

<https://github.com/SamEdwardes>

### PyOpenSci

community around scientific packages

<https://www.pyopensci.org/>

Python packaging guide call out <https://www.pyopensci.org/python-package-guide/>

### Trading & Python: THe Money Combination

Samyak Jain

@SamyakJainIND

Renko Charts vs Candlestick Charts

<https://tradewithpython.com/>

### Power To The People Who Teache ....

Sheena

""The average student tutored one to one using mastery learning techniques performed 2  std deviations better than students educatin in a calassroom envirobnment"

Mastery based learning & 1:1 tutoring

Growth vs Fixed mindset

### The End of Days [joyfully]

Madison Swain-Bowden

Minori Sanchiz-Fung poems

Kingdom of Fear

### PursuedPyBear

quick demo of ppb
