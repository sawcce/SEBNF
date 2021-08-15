- [What is the SEBNF](#what-is-the-sebnf)
  - [Basics](#basics)
    - [Defining a rule](#defining-a-rule)
    - [Literals](#literals)
  - [Complex Syntaxes](#complex-syntaxes)
    - [Groups](#groups)
    - [Or syntax](#or-syntax)
    - [Character Range](#character-range)
      - [What is a character](#what-is-a-character)
      - [Unions](#unions)
  - [Modifiers](#modifiers)
    - [Options](#options)
    - [Repetitions](#repetitions)
      - [One or more (+)](#one-or-more-)
      - [Zero or more (?)](#zero-or-more-)
      - [Specific amount or range](#specific-amount-or-range)

# What is the SEBNF

The sebnf (simplified extended backus naur form) language is an attempt at making the backus naur and extended backus naur form easier to manage, create and develop with

## Basics

### Defining a rule

```sebnf
# This is a comment
# Defining a rule

rule_name = <rule> : doc comment / inline comment
```
### Literals

How to match string literals ?

```py
# This example shows a rule representing a left parenthesis

lparen = "("
```

```py
# This example shows how to use multiple literals in a row

one_plus_one = "1" "+" "1" : matches 1+1
```

See that we're using the "1" literal multiple times ?

Though it is far from being necessary we can also make use of nested rules like this (it will come in handy later) : 

```py
one = "1"

one_plus_one = one "+" one
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
### Character Range

Matching the output of a dice like in the previous example is pretty annoying.
That's why the character range operator exists

This is the grammar for it:
```py
character_range = character ".." character : matches any character from the ASCII code of the first character to that of second character inclusive
```

#### What is a character

The charater symbol in sebnf is only used for the character range

Since the character range only accepts characters you don't need to escape them.

If you want to use a character based on its hexadecimal ASCII value you can do `$<hex value>`

#### Unions

To reproduce this regex pattern `` [a-zA-Z] `` you can just do `` a..z | A..Z `` since `` a..z `` is the equivalent of `` "a"|"b"|"c"|"d" `` ...

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

#### Specific amount or range

```py
# digit will be an imaginary rule to represent digits

# Specific amount

three_digits = digit * 3 : Matches any non-negative 3-digit integer

# Matches: "234", "000", "921"
# Doesn't match: "1234", "64", "314.1", "-562"

# Range

small_integer = digit * ..2 : Matches any non-negative integer with up to and including 2 digits

medium_integer = digit * 3..5 : Matches any non-negative integer with between 3 and 5 digits inclusive

big_integer = digit * 6.. : Matches any non-negative integer with at least 6 digits

any_number = digit * .. : Matches any non-negative integer

# note: the above also counts padded zeroes, so 0012 is seen as a 4-digit number when it's actually a 2-digit one, 12
```
