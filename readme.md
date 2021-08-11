- [What is the SEBNF](#what-is-the-sebnf)
  - [Basics](#basics)
    - [Defining a rule](#defining-a-rule)
    - [Literals](#literals)

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

