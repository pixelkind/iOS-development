# Getting a location

Before we can start reading the GPS location of the phone, we have to add some information to the `Info`. You can find the `Info`, when you click on your project name. In this example, the name is _LocationExample_. Under _Targets_ you select `Info`. Here you need to add an additional key-value pair. The `key` for the entry is `Privacy - Location When In Use Usage Description`. In the value you should add a description _why_ your app needs access to the location.

## LocationManager

In order to get a location we need to use the `CoreLocation` framework. This framework is an older Apple Framework and therefore, we want to create our own `LocationManager` to make it work with SwiftUI. First, we import the `CoreLocation` framework in order to use the GPS location and the `Observation` framework to make it easy to update SwiftUI. We use the `@Observable` keyword and create a `LocationManager` class.

```Swift
import Foundation
import CoreLocation
import Observation

@Observable
class LocationManager {

}
```

Next, we will create an instance of the `CLLocationManager` and a function to request location updates called `requestLocation`. Inside the function, we have an if-statement that checks the `authorizationStatus` of the `locationManager`. If the `authorizationStatus` is `.notDetermined`, we call `requestWhenInUseAuthorization`. This will show an alert to the user that asks for the permission to use the position. The usage description we earlier added to the `Info` is displayed here and the user can decide if they want to allow your app to access the location. If the user has allowed access earlier and not only once, we can directly call `requestLocation`.

```Swift
@Observable
class LocationManager {

    private let locationManager = CLLocationManager()

    func requestLocation() {
        if locationManager.authorizationStatus == .notDetermined {
            locationManager.requestWhenInUseAuthorization()
        } else {
            locationManager.requestLocation()
        }
    }
}
```

Until now, we don't get any updates about the position from the `CLLocationManager`. The updates will be provided using a _Delegate_, the `CLLocationManagerDelegate` that we need to add to our class. In order to fulfill the requirements, we also need our `LocationManager` inherit from `NSObject`.

In the constructor, the `init` function, we set the delegate to `self`. That means, to the object of the `LocationManager` class.

Now, we want to implement the following _delegate_ methods:

- `locationManagerDidChangeAuthorization(_ manager: CLLocationManager)`
  - This function will be called when the `authorizationStatus` is changed and you can react on it.
- `locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation])`
  - This function will be called when there is an updated location.
- `locationManager(_ manager: CLLocationManager, didFailWithError error: Error)`
  - This function will be called when there was an error while updating a location. You can use a print to check possible errors in the console.

```Swift
@Observable
class LocationManager: NSObject, CLLocationManagerDelegate {

    private let locationManager = CLLocationManager()

    override init() {
        super.init()

        locationManager.delegate = self
    }

    func requestLocation() {
        if locationManager.authorizationStatus == .notDetermined {
            locationManager.requestWhenInUseAuthorization()
        } else {
            locationManager.requestLocation()
        }
    }

    func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) {
        // This function will be called when the `authorizationStatus` is changed and you can react on it
    }

    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        // This function will be called when there is an updated location
    }

    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        // Do something in case of error
    }
}
```

Let us continue and implement the `locationManagerDidChangeAuthorization` function. Here, we want to check if the user has not _denied_ our request for access to the location. If not, we can call `locationManager.requestLocation()` here, in order to get a location.

Once, the `requestLocation` has been called, we wait until `locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation])` is called and we can take the last element from the `locations` array. That is the last position we had. In order to store it, we create a `var location` of type `CLLocation` and make it optional because initially, we don't have a location.

```Swift
@Observable
class LocationManager: NSObject, CLLocationManagerDelegate {

    private let locationManager = CLLocationManager()
    var location: CLLocation?

    override init() {
        super.init()

        locationManager.delegate = self
    }

    func requestLocation() {
        if locationManager.authorizationStatus == .notDetermined {
            locationManager.requestWhenInUseAuthorization()
        } else {
            locationManager.requestLocation()
        }
    }

    func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) {
        if locationManager.authorizationStatus != .denied {
            locationManager.requestLocation()
        }
    }

    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        location = locations.last
    }

    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        // Do something in case of error
    }
}
```

Now we can display the location in SwiftUI. We can access the `coordinate` property, that has a `latitude` and a `longitude` property.

## Display the data

In order to display the data, we build a simple view that has a `LocationManager` saved in a `@State` variable. If we have a location, we can display the `latitude` and `longitude` otherwise a short text, letting the user know about the current state.

We use the `onAppear` modifier to call the `requestLocation` method, once the view appears. And we can use the `refreshable` modifier to call it again if we use the _pull-to-refresh_ on the `ScrollView`.

```Swift
@State private var locationService = LocationManager()

var body: some View {
    ScrollView {
        Image(systemName: "globe")
            .imageScale(.large)
            .foregroundStyle(.tint)
        if let location = locationService.location {
            Text("Current Location: \(location.coordinate.latitude), \(location.coordinate.longitude)")
        } else {
            Text("No location")
        }
    }
    .padding()
    .onAppear {
        locationService.requestLocation()
    }
    .refreshable {
        locationService.requestLocation()
    }
}
```

## Reverse Geocoding

In order to get the address that belongs to a latitude and longitude coordinate, we can use the _reverse geocoder service_ from Apple. First, we create a `geocoder` property and assign a `CLGeocoder` object. Next, we add a function that will use the `async` version of the `reverseGeocodeLocation` method from the `CLGeocoder`. We can use the `Task` to execute the function in the background and wait for an answer.

```Swift
@Observable
class LocationManager: NSObject, CLLocationManagerDelegate {

    private let locationManager = CLLocationManager()
    private let geocoder = CLGeocoder()
    var location: CLLocation?
    var address: CLPlacemark?

    override init() {
        super.init()

        locationManager.delegate = self
    }

    func requestLocation() {
        if locationManager.authorizationStatus == .notDetermined {
            locationManager.requestWhenInUseAuthorization()
        } else {
            locationManager.requestLocation()
        }
    }

    func reverseGeocodeLocation(_ location: CLLocation) {
        Task {
            let placemarks = try? await geocoder.reverseGeocodeLocation(location)
            address = placemarks?.last
        }
    }

    func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) {
        if locationManager.authorizationStatus != .denied {
            locationManager.requestLocation()
        }
    }

    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        location = locations.last
        if let location {
            reverseGeocodeLocation(location)
        }
    }

    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        // Do something in case of error
    }
}
```

If we now want to for example, show the city name in the view, we can use `locality` property on the `CLPlacemark`.
