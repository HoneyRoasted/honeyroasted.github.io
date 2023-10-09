# [Fill](landing.md) Primer

## Definitions
### Injection Target
An injection target is either a
 
- Field
- Method parameter
- Constructor parameter

Injection targets are identified by "injection annotations," and have a type and a list of annotations.

### Injection Annotations
An injection annotation is an annotation annotated with `@InjectionAnnotation`,

### Matchers
A matcher is a `Predicate<InjectionTarget>`. There are some simple matcher implementations in the
`Matchers` interface, which match `InjectionTarget`s based on their type and/or annotations.

### Binding
A binding provides a mapping from `InjectionTarget`s to `InjectionResult`s, which contain the value
that should actually be injecting. Bindings can also claim or reject `InjectionTarget`s to decide which ones
they want to handle.

### Injector
An injector takes a binding and uses it to actually carry out the injections.

---
## Usage
Unless you need to do something particularly fancy, most injection can be carried out using `Injector.builder()`. For example,
an injector which binds all injectable `int`s to the value `42` would look like this:
```java
Injector.builder()
        .bind(int.class).toInstance(42)
        .build();
```
The builder also supports using generics from the [Jype](../jype/landing.md) library, so an injector which binds all
injectable `List<String>`s to `{"Hello", "World"}` might look like this:
```java
Injector.builder()
        .bind(new TypeToken<List<String>>() {}).toInstance(List.of("Hello", "World"))
        .build();
```  
You can also bind to a type and a target annotation, so an injector which binds `int`s annotated with `@MeaningOfLife` might
look like this:
```java
Injector.builder()
        .bind(int.class, MeaningOfLife.class).toInstance(42)
        .build();
```

Finally, the built `Injector` provides a few different methods to carry out injection:

- `<T> T create(Class<T>)`: creates a new instance of the given class by searching for either the default constructor, a constructor
annotated with an injection annotation, or a constructor where each parameter is injectable (annotated with an injection annotation).
- `void inject(Object)`: attempts to inject values into the given object. Fields annotated with injection annotations
will be injected into, and methods that are either annotated with an injection annotation, or which all parameters
are injectable (annotated with an injection annotation).
- `void injectStatic(Class)`: follows the exact same logic as `inject`, but targets static fields and methods.
- `<T> T createAndInject(Class<T>)`: Calls `create` on the given class, then calls `inject` on the produced object.

---
[Home](../index.md) | [Contact](../contact.md)