---
layout: single
title: "They run fast, they help us localize problems"
categories: testing
tags: testing-on-the-chair concept
---

“They run fast, they help us localize problems”.  This is how Michael Feathers defines the qualities of a good unit test. This can be hard to accomplish when running your test on a file-based database, depends on networking, is time-dependent, etc.

Let's be super clear here. Those things that slow you down, forced to have a branch not having coverage, is called a dependency! To thoroughly test your code and increase the coverage, at the same time keep or even improve the execution speed, you just need to substitute the dependencies with `custom objects`.  With a deliberate design, you can achieve concurrency in production while synchronizing in the test.

Here I will use the definition from Gerard Meszaros.

- Test Double is a generic term for any test object that replaces a production object.
- Dummy objects are passed around but not used. They are usually fillers for parameter lists.
- Fakes have working implementations but take some shortcuts (e.g., InMemoryDatabase).
- Stubs provide canned answers to calls made during a test.
- Mocks have expectations that form a specification of the calls they do and do not receive.  


For example, we try to get a product entity from the CoreData stack using the belong function. What would you do if you need to test the error alert?

```swift
class DataHandler {
	...

	func getProduct(id: ID, coreDataStack: CoreDataStack) throws -> Product {
		do {
			try coreDataStack.getProduct(id: id)
		} catch {
			self.showAlert(error)
		}
	}
}

```
You could look through the project and looking for how can make the `getProduct` function on the `coreDataStack` class to throw and error. Then some other time to just set up the persistence data. In the end, hope it throws an error.

Or, You can avoid these pitfalls by using stubs:
```swift

protocol DataBase { <--- make sure you have a protocol for the CoreDataStack to conform
	func getProduct(id: ID) throws -> Product
}

class DataHandler: DataBase { ... }

```
Creating the stubs:

```swift
class CoreDataStackThatThrowsError: DataBase {
	func getProduct(id: ID) throws -> Product {
		throws Error.myError
	}
}

```


In your test function:

```swift
func testShowErrorAlert() {
	let stubDataBase = CoreDataStackThatThrowsError()

	let error =self.dataHandler.getProduct(id: id, coreDataStack: stubDataBase)
	// test the error handlling
}

```

Stubbing can be super useful when trying to test objects that run with time. Also, it can help with testing on the object that comes externally such as from SDK.

