# Jype

- [Repository](https://github.com/HoneyRoasted/Jype)
- [Primer](primer.md)

## About

Jype is an implementation of Java's type system capable of testing assignability between types and producing type signatures.

## Modules

### Jype Main
[Javadocs](https://honeyroasted.github.io/Jype/jype-main)

The Main module contains all major type system APIs and solvers. This includes:
- Objects modelling the type structure
- Type resolution utilities for reflection, binary, and signatures
- Various type operations discussed in the java specification
- Constraint solvers for inference and compatibility
- Utilities for generating signatures and descriptors
- ...And more!

### Jype Stub
[Javadocs](https://honeyroasted.github.io/Jype/jype-stub)  

The Stub module defines a YAML DSL for building type objects and performing tests on the main module's solvers. It
is primarily used in running the main module's test suite, but could also be used to provide ways to define
types and constraints via YAML. See examples in the [main module's tests](https://github.com/HoneyRoasted/Jype/tree/main/jype-main/src/test/resources/stub_tests).

---
[Home](../index.md) | [Contact](../contact.md)