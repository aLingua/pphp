# pphp spec(?)

## Table of contents
* [What is pphp?](#what-is-pphp)
* [What's so special about pphp?](#whats-so-special-about-pphp)
  * [php vs pphp](#php-vs-pphp)
* [pphp features](#pphp-features)
* [pphp roadmap](#pphp-roadmap)

## What is pphp?

***pphp*** (**p**rocedural **php**) is a PHP-inspired procedural scripting language aimed for web development (server side scripts, websites and webapps).

## What's so special about pphp?

***pphp***'s defining characteristics are:
- **simplicity** - *pphp* has a simple, intuitive, readable syntax, allowing to spend less time figuring out your own old code or other people's code
- **compatability** - with the `compat` module you can work with your familiar php scripts in no time, you can also convert them to pphp scripts

***pphp***'s goal is to create a web development language that anyone, be it noob or pro, can pick up and lift off in no time with ease.

## php vs pphp

When compared to php *pphp* does not have the OOP, which is a source of unnecessary complexity in the target scripts. Instead of usual `class`es *pphp* introduces the concept of `module`s as groups of functions and variables similar to ones from [lua](https://www.geeks3d.com/20130906/how-to-create-a-lua-module/).

*pphp* also has readable, intuitive, ruby-like syntax, to make the process of writing scripts easier.

## pphp features

- ruby-like syntax
- procedural language
- compatability with php
- transpiling from php to pphp

## pphp roadmap

### planned

* engine with the ruby-like syntax based on php features and module concept
* compatability with apache or a custom server
* `compat` module for php compatability
* ability to convert php scripts to pphp scripts (`.pp`)

---

* package manager (*ppm*)
* ability to convert composer packages to ppm packages


### for syntax please check [syntax](https://github.com/aLingua/pphp/blob/master/spec/syntax.md)
