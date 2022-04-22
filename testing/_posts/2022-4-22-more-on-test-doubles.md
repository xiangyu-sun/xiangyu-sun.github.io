---
layout: single
title: "More on Test Doubles"
categories: testing
tags: test-toolbox
---

You are here means that you want to know more about test doubles. Examples here will help you save plenty of trouble when testing external systems or components.

Continue with the 5 types of test doubles and let's look at the examples of using them. 

## Dummy

A dummy can be anything that you passed into an API and it just works. It can be a type used in production but just with some random value. This is also what you would normally use on a day-to-day basis. 

```swift

let cartItem = CartItem(name: .productName)
self.shoppingcart.add(cartItem, .numberToIncrease)
expect(.numberToIncrease) == self.shoppingcart.getItemCount(byName: .productName)

```

## Stub

Stub overrides the original object and returns hard-coded values. In the example below. We use a StubPricer to isolate the noise from the product itself. So the cart's state is verified. 

```swift
struct StubPricer: PricerProtocol {
	func itemPrice() -> Double {
		return .stubPrice
	}
}

let cartItem = CartItem(name: .productName)

let cart = ShoppingCart(pricer: StubPricer())

cart.add(cartItem, .numberToIncrease)

expect(.stubPrice * .numberToIncrease) == cart.getItemPrice(byName: .productName)

```

## Mock

A mock can return value, but it is more often used to check the way methods are called. Strick mocks care about the order of the calls, whereas lenient mocks do not. Thus the assertion is implemented on the mock itself. It is interaction-based as you need to set expectations first.

```swift
struct MockPricer: PricerProtocol {
	var callItemPrice: Bool = false

	var expectation: (Self) -> Void

	func itemPrice() -> Double {
		self.callItemPrice = true
		return .stubPrice
	}
}

let cartItem = CartItem(name: .productName)
let pricer = MockPricer()

pricer.expectation = { mock
	expect(mock.callItemPrice) == true
}

let cart = ShoppingCart(pricer: pricer)

cart.add(cartItem, .numberToIncrease)

// run assertions
pricer.expectation()

``` 

## Spy

Spy works similarly to Mock. Return values and record calls to is the method.  It is more state-based other than interaction-based. In a sense. This looks just like a stub test.

```swift
struct LogSpy {
	var transavtionLogged: Bool
	var amountOfTransaction: Double
}

let cartItem = CartItem(name: .productName)
let logSpy = LogSpy()
let cart = ShoppingCart(logSpy)

cart.add(cartItem, .numberToIncrease)

expect(logSpy.transavtionLogged) == true
expect(.stubPrice * .numberToIncrease) == logSpy.amountOfTransaction

``` 

## Fake

Fake swaps out the original implementation with a simpler, fake implementation. It does not matter what storage is used. The result is always the same. 

```swift


let cartItem = CartItem(name: .productName)

let cart = ShoppingCart(InMemeoryStorage())

cart.add(cartItem, .numberToIncrease)

expect(cart.numberOfItems) == 1

```
