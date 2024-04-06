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
