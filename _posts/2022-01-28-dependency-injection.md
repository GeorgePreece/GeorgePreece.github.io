---
layout: "article"

title: "Dependency Injection"
description: >
    Learn how to apply an inversion of control using dependency injection
author: George Preece
category: article
tags: development
---
# {{ page.title }}

Dependency Injection (DI) is a technique to apply an _inversion of control_, where a client who wants to use a service should not create it. Instead, an injector passes the service to the client. When used appropriately, DI comes with many benefits as it naturally lends itself towards the _separation of concerns_ design principle.

```
+-----------+                                                       +---------+
| :Injector |                                                       | :Client |
+-----------+                                                       +---------+
      |                                                                  |
     [ ]                        +------------+                           |
     [ ]-------------«create»-->| s:IService |                           |
     [ ]                        +------------+                           |
     [ ]                               |                                 |
     [ ]------------------------------------------------------inject s-->|
     [ ]                               |                                 |
      |                                |                                 |
```

There are three major roles played in DI:
- **the Client** who depends on functionality provided by; 
- **the Service** that implements functionality through an interface
- **the Injector** who facilitates injecting the Service into the Client

## Injection Methods
In the previous diagram, the ambiguous term "inject" is used. This operation can happen in many different ways, but the two core approaches are [_Constructor Injection_](#constructor-injection) and [_Setter Injection_](#setter-injection). Other approaches are typically language-specific and use features such as Reflection, which allows an application to introspect itself.

Before exploring these methods, consider the following example of a client/service that does not perform an injection. When comparing this example with Constructor Injection and Setter Injection, notice how the client is responsible for constructing the service.

```
class Application {
    execute(void) : void {
        final Client client;

        client = new Client();
        // Do something with client
    }
}

class Client {
    service : IService;

    constructor(void) {
        this.service = new ServiceImpl();
    }
}
```

### Constructor Injection
As the name implies, this method uses an object's constructor to deliver the service. There are two key aspects to consider when using Constructor Injection. Firstly, since the constructor creates the client, it cannot be created without its required service(s) upfront. Secondly, it is only possible to call the constructor once; therefore, changing services after creation is impossible with this method alone.

The nature of these constraints makes Constructor Injection an excellent approach to **force** an injection (for mandatory dependencies).

The following example depicts a simple implementation of Constructor Injection.
```
class Application {
    execute(void) : void {
        final Client client;

        client = new Client(new ServiceImpl());
        // Do something with client
    }
}

class Client {
    service : IService;

    constructor(service : IService) {
        this.service = service;
    }
}
```

### Setter Injection
Setter Injection uses a setter method to inject a service which, in contrast to Constructor Injection, makes Setter Injection the preferred approach to inject **optional** dependencies. Also, if the client requires changing services post-creation, consider this injection method. 

```
class Application {
    execute(void) : void {
        final Client client;

        client = new Client();
        client.setService(new ServiceImpl());
        // Do something with client
    }
}

class Client {
    service : IService;

    setService(service : IService) {
        this.service = service;
    }
}
```