---
layout: "article"
title: "Test Doubles"
tags: development
---
# {{ page.title }}

The term "test double" was coined by Gerard Meszaros in the book [XUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/). It is used to describe a test-specific replacement for a dependent code unit. These are often used to enhance tests by verifying indirect input/output, isolating code units and increasing test execution speed.

Test doubles come in different flavours, the five most notably named variations are _dummies_, _stubs_, _spies_, _mocks_ and _fakes_. Doubles are often confused with mocks, however, a mock is simply a variation of a test double. A better programming vocabulary can greatly improve collaboration on projects when every engineer understands the same terminology.