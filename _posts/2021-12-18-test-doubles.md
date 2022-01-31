---
layout: "article"

title: "Test Doubles"
description: "Learn how to inject indirect inputs, verify indirect outputs and increase test execution speed using test doubles"
author: "George Preece"
category: article
tags: development
---
# {{ page.title }}

Writing tests often leads us to a situation where two code units interact, making testing every logical path difficult or sometimes even impossible. Test doubles alleviate this by replacing the dependent code unit with a test-specific replacement. The replacement allows us to control indirect inputs, verify indirect outputs and even increase test execution speed. Gerard Meszaros coined the term "test double" in [XUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/), describing it as a stunt double; it appears the same as the real actor but does what we instruct it.

## Direct and Indirect I/O
Making the most of test doubles requires understanding the difference between direct and indirect input/output.

**Direct I/O** is the immediate data communicated with the unit of code. That is, the data we _send_ (typically in the form of arguments), whereas the direct output is the data we receive (typically in the form of a return value).

**Indirect I/O**, on the other hand, is the data communicated with a dependency of the unit of code. To illustrate this, let us consider the below example of a simple discount calculator. Every Tuesday, there is a weekly discount where a 50% reduction is applied. On top of that, presenting a valid voucher code applies a further reduction.

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

In the above example, the arguments `amount` and `voucherCode` are direct inputs, and the variable `result` is the direct output. There is, however, more data being _indirectly input_ in the form of `Date.getWeekday()`. If inputs are uncontrolled, our test can produce inconsistent results simply because of the current weekday. However, if we could control this input, we could test all code paths consistently. The example also includes _indirect output_ when we pass `result` into `applyReduction`. Without an observation point, we may be unable to test various requirements.

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