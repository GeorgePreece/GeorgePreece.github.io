---
layout: "article"
title: "Dependency Injection"
tags: development
---
# {{ page.title }}

Dependency injection (DI) is a technique for _inversion of control_ where a client who wants to use a service should not be required to construct the service. Instead, an injector is used to pass the service to the client. DI comes with many benefits as it naturally lends itself towards the _separation of concerns_ design principle. It also promotes testability by enabling the use of test doubles.

## Injection methods
There are multiple methods in which the client can receive the service. The "standard" methods are [_Constructor Injection_](#constructor-injection), [_Setter Injection_](#setter-injection), and [_Interface Injection_](#interface-injection). I describe these as standard as they are typically supported out-of-the-box with object-oriented languages. Another common approach is to use reflection, a feature available in languages such as Java and C# that allows an application to introspect itself.
