---
layout: single
title: "Craftsmanship in coverage"
categories: testing
tags: testing-en-la-cocina coverage symptom craftsman
---

High coverage is a necessary but not sufficient condition. I think we can all agree on that.

In my work, I saw plenty UIViews are just get initialized then people call it to reach sufficient coverage to pass the PR merge condition. Why we would prefer to lie to ourselves and live in falsehood. I blame so much on our educations and our ways of working. We have been measured by metrics, and this creates a momentum that when we start to work, we aim to reach the metric other than thinking about work itself and how it defines me. Too many people say about do not attach to your work is much on the perfectionism and obsession side of the work. Seriously you are being blind if you never think about how does what you do has an impact on you. How a master becomes a master is not because he is a craftsman. It is because he doing what you think craftsmen do!

What is the craftmanship like in testing:

1. Do not look at the coverage. Ask yourself did you tested comprehensively on the code you wrote? (DO NOT be smart here). Be super honest with yourself. Write as much as a test as necessary, think about all the possible cases and not the minimum set of tests to achieve maximum coverage.

2. Now use code coverage to analyze why some code is not covered. Also look for unexpected patterns, which often indicate bugs.

3. Add tests to address the missing case you find in the previous step.

4. Repeat steps 2 and 3 until it's no longer cost-effective. If it is too difficult to test some cases, it is a perfect time to consider refactoring for improving testability. It will give you enough reasoning to tilt to testability between encapsulation.
