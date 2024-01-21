# Async await to load data

Since iOS 15 (backwards compatible down to iOS 13) we have a new way to handle concurrency using the `async` and `await` keywords. Using this, we are able to structure asynchronous code better and make it easier to read.

Using the `async` keyword, you can mark a function as asynchronous. If you want to call an asynchronous function, you need to use the `await` keyword. Let's have a look at an example:

```Swift
func loadImages() async -> [UIImage] {
  // ...load images in the background
}

let images = await loadImages()
```

Asynchronous functions can only be called from within an asynchronous function and it cannot be called from your UI directly. Therefore, we need tasks.

## Tasks

A task creates a new concurrent task in which we can execute asynchronous code. We can for example use the `Task {}` initializer.

```Swift
func loadImages() async -> [UIImage] {
  // ...load images in the background
}

var images: [UIImage] = []

Task {
    self.images = await loadImages()
}
```

Or the `task` modifier if we are in SwiftUI. The big advantage of this is, that the scope of the task is bound to the lifecycle of our SwiftUI view.

```Swift
@State private var images: [UIImage] = []

var body: some View {
  VStack {
    Text("Hello")
  }
  .task {
    self.images = await loadImages()
  }
}

func loadImages() async -> [UIImage] {
  // ...load images in the background
}
```

## Sequentially execution

If we use the `await` syntax, like in the examples above, our code will be executed sequentially.

```Swift
let result1 = await loadResult1()
let result2 = await loadResult2()
```

That means, before we start loading result2, we are waiting for result 1 to be finished.

## Parallel execution

If we want to have multiple tasks in parallel, we can use the `async let` keyword.

```Swift
async let result1 = await loadResult1()
async let result2 = await loadResult2()
```

This can be used for other things than loading data, for example scaling images, etc.

## Actors

ADD A LINK HERE!

Actors protect their states from data races by isolating data access
Concurrent access to mutable data will be prevented
Access to data must be synchronized
The actor keyword can be used like the class keyword
Actors are reference types
They do not support inheritance
