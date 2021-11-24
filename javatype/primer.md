# [JavaType](landing.md) Primer

## Definitions
### Type Parameter
A Type parameter is a type variable appearing in either a class or method declaration. For example:
```java
public class Foo<T extends Baz> {
    ...
}
```
here, `T` is a type parameter with the bound `Baz`. Similarly:
```java
public class Foo {
    
    public <K extends Number> K method() {
        ...
    }
    
}
```
here, `K` is a type parameter with the bound `Number`.

(Note that a "parameter type" means the type of a method parameter, while the "type parameters" of a method refer to the above.)

### Generic Argument
A generic argument is when a type parameter is given a value somehow. For example:
```java
List<String> str = ...;
```
here, the `List` type has the generic argument `String`.  
Generic arguments are often inferred in methods, for example:
```java
Optional<String> opt = Optional.of("Hello world");
```
here, the method `Optional#of` has the generic argument `String`, but that argument
is not explicitly declared.

### TypeInformal

In the library, "TypeInformal" means any type that can be:

- The type of a variable
- The type of a method return or a method parameter
- A generic argument

This includes references to type variables, arrays, types with generic arguments,
and wildcards.

---

## Usage
The entire library can be accessed through the `Types` class. This class has constants for all primitive types and their boxing types, as well as methods for:

- Creating types from Java's reflection types (`Class`, `java.lang.reflect.Type`, etc.)
- Building new types
- Convenience methods

Additionally, every `Type` has the following methods:

- `String signature()`: The JVM signature of the type
- `String formalSignature()`: The JVM signature of the type, as it would appear in a class declaration
- `String descriptor()`: The JVM descriptor of the type
- `String internalName()`: The JVM internal name of the type
- `String externalName`: The human-readable name of the type

Finally, `TypeInformal` has the method `TypeInformal#isAssignableTo` to determine if one type is assignable to another.
This is determined by how the java compiler allows types to be assigned, and is intended to be consistent with it. If you
discover an inconsistency, please create an issue.

---
[Home](../index.md) | [Contact](../contact.md)