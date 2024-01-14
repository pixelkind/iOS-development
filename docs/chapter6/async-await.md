# Async await to load data

Since iOS 15 (backwards compatible down to iOS 13) we have a new way to handle concurrency that is called structured concurrency. By using the `async` and `await` keywords, we are able yo structure asynchronous code better and make it easier to read.

Using the `async` keyword, you can mark a function as asynchronous. If you want to call an asynchronous function, you need to use the `await` keyword. Let's have a look at an example:

```Swift
func loadImages() async -> [UIImage] {
  // ...load images in the background
}

let images = await loadImages()
```

Asynchronous functions can only be called from within an asynchronous function and it cannot be called from your UI directly. Therefore, we need tasks.

## Tasks

```Swift
func loadImages() async -> [UIImage] {
  // ...load images in the background
}

var images: [UIImage] = []

Task {
    self.images = await loadImages()
}
```

Scope is the SwiftUI view

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

await

## Parallel execution

async let

This can be used for other things than loading data, for example scaling images, etc.

## Actors

Actors protect their states from data races by isolating data access
Concurrent access to mutable data will be prevented
Access to data must be synchronized
The actor keyword can be used like the class keyword
Actors are reference types
They do not support inheritance
