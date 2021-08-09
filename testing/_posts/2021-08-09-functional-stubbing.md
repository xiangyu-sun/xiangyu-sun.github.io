---
layout: single
title: "Functional stubbing"
categories: testing
tags: testing-on-the-chair functions
---

As we are in 2021, everybody knows what POP is. if you do not. It represents protocol-oriented programming, Apples has shown an interesting technique to mock LocationManger by making it conforms to your protocol. Thus you can create a mockLocationManager and use it as a double in your test.

The same can be done for `FileManager`. But the question is: will you spend that much time copying all those functions signatures on it? Say you have a function like below:

```swift

class MovieLocator {
    func loadTheMoview(path: String) -> Bool {
        if FileManager.default.fileExists(atPath: path) {
        	doSomething()
        } else {
        	domSomthingElse()
        }
    }
}

```
How will you test it?

Take the lesson from TOT. It is safer and faster to parameterize the built-in: 

```swift

class MovieLocatorTestable {
    func loadTheMoview(path: String, fileChecker: (String) -> Bool = FileManager.default.fileExists) -> Bool {
        if fileChecker(path) {
            doSomething()
        }else {
            doSomethingElse()
        }
    }
}

func test() {

    let actualSomething = MovieLocatorTestable().isMovieExist(path: path) { path
        true
    }
    assrt(actualSomething == something)
    
    
    let actualSomethingElse = MovieLocatorTestable().isMovieExist(path: path) { path
        false
    }
    assrt(actualSomethingElse == somethingElse)

}


```

Act, arrange, assert are in one place!  Great!
