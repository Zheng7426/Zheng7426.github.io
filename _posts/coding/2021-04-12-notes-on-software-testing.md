---
layout: post
title: "Notes on software testing"
date: 2021-04-12 00:00:00 -0000
categories: coding 
---

Software testing includes manual testing and automated testing. The purpose of this process is to check the completeness and whether a program's behavior is consistent with its intended objective. When these two things differ, then we might have some *bugs* to fix. Bugs are the flaws or errors in a program, and they often lead to unexpected behaviors.  

In the context of web development, tests are written in code. There is *implementation code* for web applications and *test code* which is intended for testing purposes. These two sorts of code would normally be stored in the same place.  

Generally, a web application would have more than one feature. Thus, there might be several tests needed in total. A set of tests is called a **test suite**. Executing a automated test suite is relatively fast and reproducible, compared with manual testing. You may run it by using `npm test` command, assuming you have already configured the filenames for testing code in the **package.json** file. When you add a new functionality or feature that causes one of the earlier functionality to fail the test, that earlier functionality has *regressed*.  




