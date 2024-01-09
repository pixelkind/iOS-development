# Environment

Sometimes you need a state property or a state object that is available all over your app. In SwiftUI we can use the `Environment` for this use-case. A value or an object in the environment is accessible everywhere in our SwiftUI view-tree, but is only defined once. Therefore, we are following the _single source of truth_ principle and we have an easy way to share it, without over-using _binding_.

For many apps this is particular useful, if they rely on a single data source.

This is how you can create an environment object:

```Swift
@State private var deciderModel = DeciderModel()

var body: some Scene {
    WindowGroup {
        ContentView()
            .environment(deciderModel)
    }
}
```

Often, environment objects are created in the _root_ of your view hierarchy.

And this is how you can access the object in a view:

```Swift
@Environment(DeciderModel.self) private var deciderModel
```

Of course, it works with different types of objects, according you must change the type after the `@Environment` property wrapper.

Here you can find more information about the environment property wrapper:

ADD MORE LINKS HERE

Let's move on to Navigation in SwiftUI.
