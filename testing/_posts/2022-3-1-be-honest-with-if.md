---
layout: single
title: "Be honest with if"
categories: testing
tags: testing-en-la-cocina coverage symptom craftsman
---

Here is another topic when we start to chat about statement coverage vs branch coverage. Well-tested code has good statement coverage but not vice versa. 

Statement coverage will not be sufficient when testing branches and loops.

Here are some cases that branch coverage and statement coverage aren't the same:


```swift
func addProduct(product: Product) {
	product.count += 1
	if product.eligibleForTwoForOne {
		product.count += 1
	}
	self.notifyUI.send()
}

```

when you write the test for them, aren't they tempting that you only need to test the 2x1 case so your quality gate just gives you 100% coverage. But, did you test the case if the product is not eligible for 2x1? 

```swift
func getProductPrice(products: [Product]) {
	products.filter(!\.isFree).map(.price).reduce(0,+)
}

```

To have full coverage on the above function, you do not even need to have a product that isFree or not. an empty array would be sufficient to generate a statement coverage. The branch coverage here will be having a product that is free and not free and when the array is empty. 

Remember every if has an else, boolean has two values. 

When you write a test, you should cover all the edges in a control flow graph.