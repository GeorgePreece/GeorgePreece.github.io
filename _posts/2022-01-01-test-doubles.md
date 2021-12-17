---
layout: "article"
title: "Test Doubles"
---
# {{ page.title }}

The term "test double" was coined by Gerard Meszaros in the book [XUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/). The term describes a test-specific replacement for a dependent code unit. These are often used to enhance the quality of tests by isolating code units, verifying indirect input/output and increasing test execution speed.

Test doubles come in different flavours, the five most notably named variations are [_dummies_](#dummy-object), [_stubs_](#test-stub), [_spies_](#test-spy), [_mocks_](#mock-object) and [_fakes_](#fake-object). Doubles are often confused with mocks, however, a mock is simply a variation of a test double. It is important to improve our programming literature as it can greatly improve collaboration on projects when all the engineers understand the same terminology. 

## Indirect input/output
In order to truly understand test doubles, you need to understand (in the context of testing) what direct and indirect input/output is.

Typically when you write a unit test, the code unit you are testing (also known as the System Under Test, or SUT). is dependent on another unit. Let's use the following example to illustrate this.

```
function calculateTax(const Decimal rate) : Currency {
    
}
```


## Dummy Object
Dummy objects are used to satisfy calling methods where a object parameter is required but never used by the method. It can be as simple as a null object reference or an instance of the required object type.

## Test Stub


## Test Spy
## Mock Object
## Fake Object