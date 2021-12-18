---
layout: "article"
title: "Test Doubles"
tags: development
---
# {{ page.title }}

When writing tests, we often find ourselves in a situation where the code unit we are testing interacts with another. This can make testing every logical path difficult or sometimes even impossible. Test doubles alleviate this by replacing the dependent code unit with a test-specific replacement. This replacement can allow us to inject indirect inputs, verify indirect outputs and even increase test execution speed. The term "test double" was coined by Gerard Meszaros in the book [XUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/) where it was described as a stunt double; it appears the same as the real actor but it does what we instruct it to.

## Direct and Indirect I/O
To understand the power of test doubles, you first need to understand the difference between direct and indirect input/output. 

**Direct I/O** can be summarised as the immediate data communicated with the code unit. So, direct input is the data we _send_ to the code unit (typically in the form of arguments), whereas, direct output is the data we _receive_ (typically in the form of a return value). 

**Indirect I/O**, on the other hand, is the data communicated with a _dependency_ of the code unit. To illustrate this let's consider a <DESCRIBE EXAMPLE HERE>: 

```
TO-DO: Write code example
```

In the above example, the argument `amount` is the direct input and the return value `result` is the direct output. There is, however, more data being _indirectly input_ in the form of `foo`. This is important because, if uncontrolled, our test can produce inconsistent results simply because of the current weekday. If we were able to control this input, we could consistently test both code paths. We also have data being _indirectly output_ from the unit (`bar`). If we do not have an observation point to this, then we are usually left with untested requirements.

## Variations
Test doubles come in different flavours, each bringing their distinct uses and benefits to the table. You can think of "double" as a generic/umbrella term for the different types of variations. The five most notable named variations are [_stubs_](#test-stub), [_spies_](#test-spy), [_mocks_](#mock-object), and [_fakes_](#fake-object).

### Test Stub
Test stubs allow us to control the indirect inputs of a test. Essentially, any API requests made to a test stub are met with a pre-programmed response allowing us to exercise previously untested code paths.

### Test Spy
Test spies allow us to verify the indirect outputs of a test. They record invocations that can be used at the end of the test to verify that the correct data was sent. Spies are commonly used to extend existing tests as they do not alter the behaviour of the code unit but instead allow us to add an extra observation point. 

### Mock Object
Mock objects are a powerful variation of test doubles as they allow us to both control indirect inputs and verify indirect outputs. At the beginning of the test, we pre-programme the mock object with responses (similar to stubs) along with expected invocations (including the data). During the test, whenever the mock is invoked it will compare the data it received with the pre-defined expectations. If there is a mismatch, the assertion will fail and ultimately fail the test.

### Fake Object
Fake objects are used to substitute dependencies that are unavailable or cause slow tests. They are lightweight implementations providing the same functionality as the original. A common example is to replace a disk-based data store with an in-memory representation. This in-memory data store is not designed for end-user consumption and thus lacks characteristics such as scalability and functionality. But, in turn, will drastically increase test execution speed.