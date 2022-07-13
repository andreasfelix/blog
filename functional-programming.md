# Functional Programming (Declarative Programming)

## What is Functional Programming?

Is a collection of loosely coupled ideas. Most common definition is:

* avoid mutation
* avoid side effects (pure functions)

But people also assosiate it with:

* strong type system
* pattern matching
* algebraic data types
* no shared state
* prefer expressions over statements
* iterators
* higher-order function (either receive a function as an argument or return a function)

## What is a Pure Function?

* has no internal state
* does not have side effects (does not change some global state)
* always produces same output for same input
* can in theory be replaced by a (huge) lookup-table

## Digression: What is object-oriented programming?

* encapsulation: mix state and behavior
* inherently stateful: methods are impure functions that mutate a shared state

## Advantages

* easy to test, as functions return always the same output for same inputs
    * you don't have to initialize a certain state, to run tests
* code becomes easy to reason about
* less error-prone
* easier to refactor. pure functions don't have cross-cutting concerns
* less optionated: pure functions are just transformations. they take some inputs and produce outputs. for OOP there a million ways to compose classes and if you don't get it right on the first try, you usually end up with a mess
* better for multi-threaded environments (inherently parallelizable)

## Disadvantages

* many popular languages don't support a functional style very well
* you have to fight the language and the libraries to implement it right
* e.g. Python has some features functional common in functional languages like list comprehensions but is in the end a imperative language
* e.g. if the language does not support function chaining expressions might be hard to read (you have to read from inside out)

## Statements vs Expressions

* statements are imperative 
    * they don't have a return value, but perform a side-effect (e.g. bind a name)

```python
if x > 2:
    y = 4
else:
    y = 5
```

* expressions are declarative
    * they describe a transformation

```python
y = 4 if x > 2 else 5
```

## You can't do anything useful without side-effects

* idea is not to use no sideeffects but don't use all over the place

## Examples

Check there is at least one uppercase, lowercase, and one digit charactar in password:

```python
def is_valid(password):
    has_upper = False
    has_lower = False
    has_digit = False

    for char in password:
        has_upper |= char.isupper():
        has_lower |= char.islower():
        has_digit |= char.isdigit():
    return has_upper and has_lower and has_digit
```

```python
is_valid = lambda password: all(
    any(map(func, password)) 
    for func in [str.isupper, str.islower, str.isdigit]
)
```

```elm
isValid password = 
    [ Char.isUpper, Char.isLower, Char.isDigit ]
        |> List.all (\func -> String.any func password)
```
