---
layout: default
title: FuncSS Specification Index
---

## Specification

The FuncSS specification is organized in modules and levels, similarly to the CSS specification. Currently there are four modules, and all of them have only Level 1.

* The [**FuncSSLang**](FuncSSLang/1/WD/) module defines the syntax and semantics of the language.
* The [**FuncSSCompiler**](FuncSSCompiler/1/WD/) defines the API and configuration of the compiler.
* The **FuncSSApi** defines the client-side API of JavaScript bindings. This is a group of mutually exclusive modules, called **flavors**, of which currently only one is being developed

    - The [**FuncSSApi Vanilla**](FuncSSApi/1/Vanilla/WD/) is the flavor optimized for jQuery users and Meteor users.

    - In the future, there could be other flavors optimized for different libraries.

* The [**FuncSSLib**](FuncSSLib/1/WD/) defines the FuncSS runtime library.

These documents can have maturity levels of *Working Draft*, *Candidate Standard* and *Standard*. Currently all of them are in the Working Draft maturity level.
