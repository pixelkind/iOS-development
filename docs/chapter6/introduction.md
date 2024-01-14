# Loading data

Loading data is very common in apps and something you will do regularly. Since many things can have an impact on the time it takes to load something, for example the internet connection or the size of the data, we will use a non-blocking way of loading. If you want to write code that is running asynchronous you are using concurrency in Swift.

## Concurrency

Concurrency is a combination of asynchronous code and parallel code. Asynchronous code can be suspended an resumed, for example loading data. Parallel code is code that can in simultaneously if you have multiple cores in your processor, for example scaling a large image.

Swift offers us a convient way to deal with concurrency in iOS. [Here](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/concurrency/) can you read more about concurrency in Swift.

In the following parts, we will have a look how we handled concurrent code before iOS 15 and how we handle it now. You might encounter the _old_ way of handling concurrency, therefore it is good to know how it works. We start with the pre iOS 15 version.
