- [What is the SEBNF](#what-is-the-sebnf)
  - [Basics](#basics)
    - [Defining a rule](#defining-a-rule)
    - [Literals](#literals)
  - [Complex Syntaxes](#complex-syntaxes)
    - [Groups](#groups)
    - [Or syntax](#or-syntax)
  - [Modifiers](#modifiers)
    - [Options](#options)
    - [Repetitions](#repetitions)
      - [One or more (+)](#one-or-more-)
      - [Zero or more (?)](#zero-or-more-)

# What is the SEBNF

The sebnf (simplified extended backus naur form) language is an attempt at making the backus naur and extended backus naur form easier to manage, create and develop with

## Basics

### Defining a rule

```sebnf
# This is a comment
# Defining a rule

rule_name <rule> : doc comment / inline comment
```
### Literals

How to match string literals ?

```py
# This example shows a rule representing a left parenthesis

lparen "("
```

```py
# This example shows how to use multiple literals in a row

one_plus_one "1" "+" "1" : matches 1+1
```

See that we're using the "1" literal multiple times ?

Though it is far from being necessary we can also make use of nested rules like this (it will come in handy later) : 

```py
one "1"

one_plus_one one "+" one
```

## Complex Syntaxes

### Groups

This treats everything inside the group as one expression (will be useful later)

```py
full_name = ("SEBNF" "simplified extended backus naur form")
```

### Or syntax

```py
# Matches an output from a dice

dice = 
  "1"
| "2"
| "3"
| "4"
| "5"
| "6"
```

## Modifiers

SEBNF has modifiers similar to regex (+, *, ?)

### Options

This modifier is used to represent an optional expression

```py
# SEBNF code to represent an imaginary function declaration (identifier and arguments are imaginary)

function_head = identifier "(" arguments? ")"
```

### Repetitions

#### One or more (+)

```py
# digit will be an imaginary rule to represent digits

integer = digit+ : Matches any expression containing one or more digits

# Matches : "0", "24345904" ...
# Doesn't match : "0 0 9", "3 3", " 9089" ...
```

#### Zero or more (?)

```py
# digit will be an imaginary rule to represent digits

integer = digit+ : Matches any expression containing zero or more digits

# Matches : "", "0", "24345904" ...
# Doesn't match : "0 0 9", "3 3", " 9089" ...
```