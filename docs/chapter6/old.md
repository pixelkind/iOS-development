# Old concurrency patterns

Before iOS 15, the most common ways to handle concurreny was by using the delegation pattern or completion handler.

## Delegation pattern

You can use the delegation pattern to call a function on a specific object once a long lasting job has finished. For example, if we want to get a GPS location we need to wait until the GPS module has found a location. In order to do that, the object that should be called needs to implement a _delegate protocol_. Let us have a closer look at the location example. In this case, our class needs to implement the `CLLocationManagerDelegate` and need to set the `delegate` property of the object that executes the job to `self`. This tells the object that it should call our function when the job has been updated.

On our class, we implement some or all of the functions from the delegate. The `CLLocationManagerDelegate` has for example the `func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation])` or the `func locationManager(_ manager: CLLocationManager, didFailWithError error: Error)`. Please note, that the following example is not a complete implementation. You can check out the _Getting a location_ example later for a fully implemented example.

```Swift
class LocationManager: NSObject, CLLocationManagerDelegate {

    private let locationManager = CLLocationManager()

    override init() {
        super.init()

        locationManager.delegate = self
    }


    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        // Do something when there is a new location
    }

    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        // Do something in case of error
    }
}

```

## Completion handler

Another way to handle concurrency, besides the delegation pattern, is the usage of _completion handlers_. It is a closure, an anonymous function that will be called once a long lasting job has finished. For example, loading data from the internet.

The example we will look at is from the `URLSession` class. It is used to load data. First, let's have a look at the function. You can see a parameter called `completionHandler` and it takes a closure with an optional `Data`, `URLResponse`, and `Error` object. When this function is executed we can check the status and if the loading operation was successful, we can use the data.

```Swift
func dataTask(with url: URL, completionHandler: @escaping (Data?, URLResponse?, Error?) -> Void) -> URLSessionDataTask
```

Let's have a look how an implementation would look like. As you see, we can just _ignore_ the `URLResponse` by giving it no parameter name. After we make sure that the `Data` object exists, we can use the data, before we use a `DispatchQueue.main` to, for example, update the UI. Please note, this function might be executed in another than the main thread.

```Swift
let task = URLSession.shared.dataTask(with: url) { [weak self] (data, _, error) in
    guard let data else {
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
