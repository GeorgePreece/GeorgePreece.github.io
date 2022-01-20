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
     [ ]                        +------------+                           |
     [ ]-------------«create»-->| s:IService |                           |
     [ ]                        +------------+                           |
     [ ]                               |                                 |
     [ ]------------------------------------------------------inject s-->|
     [ ]                               |                                 |
      |                                |                                 |
```

## Injection Methods
In the previous diagram, the ambiguous term "inject" is used. This operation can happen in many different ways, but the three most common approaches are [_Constructor Injection_](#constructor-injection), [_Setter Injection_](#setter-injection), and [_Interface Injection_](#interface-injection). Another approach is through reflection, a feature available in languages such as Java and C# that allows an application to introspect itself.

### Constructor Injection
As the name implies, this method uses an object's constructor to deliver the dependency. Constructor injection is an excellent approach to forcing an injection; the injector **cannot** construct the client without the required dependencies. This method may be preferred if a dependency is mandatory for the client to function.

The below example depicts a simple example of constructor injection.
```
class Application {
    execute() : void {
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
In contrast to constructor injection, Setter injection is helpful when a dependency is not required for the client to function. Adding optional dependencies to a constructor would add unnecessary clutter and is typically better suited in a setter method. 

```
class Application {
    execute() : void {
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

### Interface Injection