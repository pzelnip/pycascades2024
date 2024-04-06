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
