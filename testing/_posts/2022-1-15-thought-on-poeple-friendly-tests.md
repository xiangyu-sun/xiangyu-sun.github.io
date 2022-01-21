---
layout: single
title: "Thoughts on human-friendly tests"
categories: testing
tags: testing-en-la-cocina symptom
---

We write code for our collaborators to understand. If it is just you, why bother yourself to give the proper naming to vars and functions. I call this the selfish and shortsighted coder. As long as the code works, we do not need to care about readability or maintainability.  Soon he will find out he does not understand why he wrote some lines of code. no good structure, no way to understand a function by its naming, not documentation.  (if he is lucky, not unit tests).
He will use a few days to re-familiar himself with his work.  If it is someone else trying to get the code? maybe double that time?

Back to tests. Here is what I think of the basic mindsets of writing tests:

- *When someone else works on the code you wrote, while they understand what went wrong just by reading the test function and error/assertion message?* Test gives your so man benefits, better structure of the code, the confidence of making changes, and at least a documentation of the behavior you are testing. It is always good to think about how you will be able to fast diagnose the point of failure when you write test function names and failure messages. 


- *Opinionated test names like `testMethodDoesSomething` can be more helpful than `testMethod`*. And this drill down to be clear on what is the behavior you are testing when you write the code. 

- *Great test messages not only identify the actual behavior but also the expected behavior*. `Should` is a handy word to use in messages – it clarifies what expected behavior didn't actually happen.

- *Always try to assert using isEqual*. When people use `contains`, `first`, `last` to just test an element inside an array, by a very large chance this test will be flaky or hide bugs in the future. Always be accurate in the assertion. In our case, if you have to use first, add another assertion on the count of the count == 1 too. Control your environment is the key to confidence.  