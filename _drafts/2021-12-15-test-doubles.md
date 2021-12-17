---
layout: "article"
title: "Test Doubles"
tags: development
---
# {{ page.title }}

When writing tests, we often find ourselves in a situation where the code unit we are testing interacts with another. This can make testing every logical path difficult or sometimes even impossible. Test doubles alleviate this by replacing the dependent code unit with a test-specific replacement. This replacement can allow us to inject indirect inputs, verify indirect outputs and even increase test execution speed. The term "test double" was coined by Gerard Meszaros in the book [XUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/) where it was described as a stunt double; it appears the same as the real actor but it does what we instruct it to.

## Variations
Test doubles come in different flavours, each bringing its own uses and benefits to the table. You can think of "double" as a generic/umbrella term for the different types of variations. The five most notable named variations are _stubs_, _spies_, _mocks_ and _fakes_.