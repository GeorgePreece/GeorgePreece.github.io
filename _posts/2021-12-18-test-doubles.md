---
layout: "article"

title: "Test Doubles"
description: "Learn how to inject indirect inputs, verify indirect outputs and increase test execution speed using test doubles"
author: "George Preece"
category: article
tags: development
---
# {{ page.title }}

Unit testing is often tricky when two or more units interact. This can make testing each logical code path difficult or sometimes even impossible. 

Test doubles alleviate this by substituting dependencies with test-specific replacements. These replacements enable us to exercise "untestable" code paths, increase test execution speed, and more. Gerard Meszaros coined the term “test double” in [XUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/). Gerard described them as stunt doubles—they appear the same as the actors but are trained to perform specific stunts for the scene that the actor would not normally do.

## Indirect Input/Output
When we write a unit test, we send data (typically in the form of arguments) to the unit and receive data (typically as a return value) back to the test for verification. This is direct input and output, respectively.

Indirect input/output, on the other hand, is the data communicated to the unit via a dependency. This is naturally much harder to control and verify.

To illustrate this, let us consider the below example of a simple discount calculator. Every Tuesday, there is a weekly discount where a 50% reduction is applied. On top of that, valid voucher codes allow for further reductions.

```
calculateDiscount(amount : Currency, voucherCode : String) : Currency {
    result = amount;

    if(Date.getWeekday() == Date.TUESDAY) {
        result *= 0.50;
    }

    if(voucherCode != null) {
        result = voucherService.applyReduction(voucherCode, result);
    }
}
```

In the above example, the arguments `amount` and `voucherCode` are direct inputs, and the variable `result` is the direct output. There is, however, more data being _indirectly input_ in the form of `Date.getWeekday()`. Without control of this input, our test can produce inconsistent results simply because of the current weekday. However, if we could specify the weekday for the test, we could exercise all code paths consistently. We could even test scenarios that would be impossible to replicate ordinarily, such as a null weekday.

The example also includes _indirect output_ when we pass `result` into `applyReduction`. Without an observation point (the ability to verify the value of result before it reaches the dependency), we may be unable to test various requirements.

## Variations
Test doubles come in different flavours, each bringing its different uses and benefits to the table. A "double" is essentially an umbrella term encompassing the different variations. The five most notable variations are [_stubs_](#test-stub), [_spies_](#test-spy), [_mocks_](#mock-object), and [_fakes_](#fake-object).

### Test Stub
Test stubs allow us to control the indirect inputs of a test. The stub responds to invocations with pre-programmed outputs, allowing us to control the test execution path. Being in control of the execution path enables us to build more consistent tests and exercise previously untested paths.

### Test Spy
Test spies allow us to verify the indirect outputs of a test. They record invocations that can be used at the end of the test to verify that the correct data was received. Spies do not alter the dependency behaviour, making them well-suited for test cases with irreplaceable dependencies.

### Mock Object
Mock objects are a powerful variation of test doubles as they allow us to control indirect inputs and verify indirect outputs. During the test setup, we pre-programme the mock object with responses (similar to stubs) along with expected invocations. When invoked, the mock will compare the data it receives with its pre-defined expectations. If there is a mismatch, the assertion will fail and ultimately fail the test.

### Fake Object
Fake objects substitute dependencies that are unavailable or cause slow tests. They are lightweight implementations providing (mostly) the same functionality as the original. A typical example is to replace a disk-based datastore with an in-memory representation. The fake datastore is explicitly built for tests and may lack characteristics such as scalability and functionality. Performance, however, will increase exponentially.