---
layout: "article"
title: "Dependency Injection"
tags: development
---
# {{ page.title }}

Dependency injection (DI) is a technique for _inversion of control_ where a client who wants to use a service should not be required to construct the service. Instead, an injector is used to pass the service to the client. DI comes with many benefits as it naturally lends itself towards the _separation of concerns_ design principle. It also promotes testability by enabling the use of test doubles.