---
layout: single
title: "Naming Unit Tests Responsibly"
categories: testing
tags: testing-on-the-chair unit-test
---

Naming, a result of one man's creativity result. But, to serve the function of communication, most of the time, it can take a whole day to just talking about preferences.

Before we start, you have an above-average understanding of what is BDD and is TDD. The former normally is perceived as an act of exercising integration test while the latter of exercising Unit Test. Nowadays, most of the teams would just embrace `Quick and Nimble` for BDD and `XCTest` for TDD. *, of course, lots of devs think to use a BDD framework to write Unit Test is also a good idea 😑 *

An object should have a similar set of test functions that describes the responsibility of the object.  Here, we will be mainly talking about namings in XCTest. 

The tests emphasizes the object's responsibilities (or features) rather than public methods and inputs/output. This makes it easier for future engineers who want to know what it does without having to delve into the code.

These naming conventions can help point out smells. For example, when it's hard to construct a sentence where the first word is the class under test, it suggests the test may be in the wrong place. And classes that are hard to describe in general often need to be broken down into smaller classes with clearer responsibilities.