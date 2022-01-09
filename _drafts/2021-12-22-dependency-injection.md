---
layout: "article"
title: "Dependency Injection"
tags: development
---
# {{ page.title }}

Dependency Injection (DI) is a technique to apply an _inversion of control_, where a client who wants to use a service should not create the service. Instead, an injector passes the service to the client. When used appropriately, DI comes with many benefits as it naturally lends itself towards the _separation of concerns_ design principle.

```
+-----------+                                                       +---------+
| :Injector |                                                       | :Client |
+-----------+                                                       +---------+
      |                                                                  |
     [ ]                         +-----------+                           |
     [ ]--------------«create»-->| s:Service |                           |
     [ ]                         +-----------+                           |
     [ ]                               |                                 |
     [ ]------------------------------------------------------inject s-->|
     [ ]                               |                                 |
      |                                |                                 |
```

## Injection Methods
In the previous diagram, the ambiguous term "inject" is used. This operation can happen in many different ways, but the three most common approaches are [_Constructor Injection_](#constructor-injection), [_Setter Injection_](#setter-injection), and [_Interface Injection_](#interface-injection). Another approach is through reflection, a feature available in languages such as Java and C# that allows an application to introspect itself.

### Constructor Injection
### Setter Injection
### Interface Injection