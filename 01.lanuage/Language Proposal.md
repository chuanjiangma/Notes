# A Language Blueprint

[toc]

## Introduction

An AOT, static type, type safe language. Providing `struct` to support value type extending. And provide `class` to support reference type extending. Provide `trait` for both all type except function type. Support generic paradigm for struct, trait, function, class.

In first step, we will use llvm as backend for its well support.

In some cases, such as web, we need to translate the source to javascript, to reuse the libraries and enbrace the ecosystems.

## Type system

#### Value Type

##### Primitive Type

- int
  - uint8
  - uint16
  - uint32
  - uint64
  - int8
  - int16
  - int32
  - int64
- float
  - float16
  - float32
  - float64
- struct
- function type

#### Reference Type

- class

#### Trait

Provide function extension ablity for value type, except function type

#### Generics

Support struct, function, trait and class.

### Primitive type

#### `int` type: integer

Use keyword `int` to represent integer type. Ideally, compiler will automaticly infer which int type is. Also you can determine the length by using specific integer type like `int32`, `int16` and so on. In most case, compiler will generate `int32` type as default.

#### `float` type: float number

Like `int` type, use keyword `float` to represent float number type. Ideally, compiler will automaticly infer which float type is, both for type matching and better performance optimization. `float32` will be the default float type.

#### `struct` type

`struct` type is a kind of value type in this language. And it is a collection of variable including function. Basicly struct will only include variables. To support function as a member, we will borrow `trait` feature.

`struct` enable you to define a user-defined value type.

#### `function` type

We want to support function type as a kind of 1st-class citizen like `int`,  `float`,  `struct` and  `class`, which means this language will be like a kind of none-pure functional language. `function` type can be function parameter, return type of a function, in another word, can be a variable type.

### Reference Type: `class`

`class` type enables you to define a user-defined reference type. Our `class` only permits **single inheritance** to simplify the type system, which also help developer avoid **diamond problem**.

All above will be the basic script of our type system.

## Package Management

### Access Control

Support access control between packages. Provide keyword  `internal` and `external` to hint the compiler that the access of the element. 

> TODO: the keyword: internal and external may not be so suitable.

### Packages Imports

A pakcage will be build to a `.a`  or `.so` file and a symbol list file, in which every symbol is well tagged with right type. This file includes all `external` accessable declarations of the package.

Since the symbol list file will be a binary file, we will provide dump tool or ablity of compiler for previewing.



