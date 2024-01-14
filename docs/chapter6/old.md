# Old concurrency patterns

Before iOS 15, the most common ways to handle concurreny was by using the delegation pattern or completion handler.

## Delegation pattern

```Swift

```

## Completion handler

One example for the usage of completion handler is the `URLSession` class.

```Swift
func dataTask(with url: URL, completionHandler: @escaping (Data?, URLResponse?, Error?) -> Void) -> URLSessionDataTask
```

```Swift
let task = URLSession.shared.dataTask(with: url) { [weak self] (data, _, error) in
    guard let data = data else {
        return
    }
    // Do something with the data

    DispatchQueue.main.async {
        // Do something on the main thread, for example update UI
    }
}
task.resume()
```

[Here](https://developer.apple.com/documentation/foundation/urlsession/1410330-datatask) can you find the documentation about it. `URLSession` offers different ways of handling concurrency, besides a solution with a completion handler it also offers a version using the new approach with async-await. Let's check that out next.
