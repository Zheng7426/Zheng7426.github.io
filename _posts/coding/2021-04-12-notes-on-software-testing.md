---
layout: post
title: "Notes on software testing"
date: 2021-04-12 00:00:00 -0000
categories: coding 
---

Software testing includes manual testing and automated testing. The purpose of this process is to check the completeness and whether a program's behavior is consistent with its intended objective. When these two things differ, then we might have some *bugs* to fix. Bugs are the flaws or errors in a program, and they often lead to unexpected behaviors.  

In the context of web development, tests are written in code. There is *implementation code* for web applications and *test code* which is intended for testing purposes. These two sorts of code would normally be stored in the same place.  

Generally, a web application would have more than one feature. Thus, there might be several tests needed in total. A set of tests is called a **test suite**. Executing a automated test suite is relatively fast and reproducible, compared with manual testing. You may run it by using `npm test` command, assuming you have already configured the filenames for testing code in the **package.json** file. When you add a new functionality or feature that causes one of the earlier functionality to fail the test, that earlier functionality has *regressed*.  

### Test Driven Development

1. Add a test before writing the functionality that is to be tested

2. Run the test. The new test should fail for expected reasons

3. Write the simplest code that passes the new test

4. All tests should now pass

5. Refactor as needed, using tests after each refactor to ensure that functionality is preserved

6. Repeat this development cycle

* Three phases of TDD: Red -> Green -> Refactor  

### Unit Testing

The purpose of unit testing is to isolate each aspect of the program to determine whether they would lead to expected behaviors.  

### Integration Testing

Aggregate the isolated pieces of the program to determine if these pieces work well together.  

### Mocha

Test frameworks allow developers to automate their tests. [Mocha](https://mochajs.org/) is a JavaScript test framework running on major JavaScript environments. Mocha as a package can be installed via npm(So you ought to have Node.js installed first). The following content introduces how to install it step by step:

1. `npm init` to initialize project and to create **package.json** file.

2. `npm install mocha -D`, note that the package would be stored in the **node_modules** folder. `-D` would indicate mocha under the `devDependencies` object of the packge.json file.  

3. Execute Mocha. Then type `npm test` to run automated test.  

```
  "scripts": {
    "test": "mocha"
  }
```

`describe` function is normally used to place tests together. While `it` function is used to define specific tests, they may be nested under `describe` functions. Both functions accept two arguments: a descriptive string indicating the purpose of the test context, and a subsequent callback function to carry out detailed tasks.

Within a test itself, that is, inside the `it` callback function, `assert.ok()` method could help you compare expected outcome and actual outcome, and throw error as needed. To write the test this way, first you need to import Node.js' assert module(CommonJS module style):  
`const assert = require('assert');`  
If `assert.ok(condition)` evaluates to false, an error message would be reported to Mocha and then be logged to the console.  

It might be useful to separate a test into four phases:  

1. setup - determine what variables, objects your test would depend on.  

2. exercise - Run the features you are trying to test

3. verify - use `assert` function to test whether the result of the previous step meets the expectations

4. teardown - If there are modifications to the environment, for example, a read and write permission (`chmod ---`) of a file changes -- they can be reset before the next test executes.

The following are some expressive methods from `assert` function:

* `assert.equal()` for loose comparison between two values (==)

* `assert.strictEqual()` for strict comparison between two values (===)

* `assert.deepEqual()` for comparing two objects or arrays

* `assert.notEqual()` for comparing between two values (!==)  


























