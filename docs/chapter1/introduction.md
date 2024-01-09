# Introduction to SwiftUI

SwiftUI is a declarative UI-framework.

## The boilerplate

When you create a new project using Xcode, it will create some example code for you. In this part, we will have a short walkthrough the code. No worries, if you don't understand everything yet. We will explain and cover all of it. And if you have open questions, feel free to ask them on Canvas, during the lecture, or in the labs.

If you open Xcode and create a new project, it will create some starting code inside the `ContentView` file for you that looks like the following:

```Swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text("Hello, world!")
        }
        .padding()
    }
}

#Preview {
    ContentView()
}
```

- The first thing that is happening here, is that it imports the SwiftUI framework.
- Next, it defines a `struct` that inherits from `View`. Every view in SwiftUI is a `struct`. That means, it is a value-type and immutable. You don't have a reference to a specific view. In a declarative approach, you don't change views directly. Instead, you define a view for a specific state and if the state changes, the view get re-evaluated and changes according to the changed state.
- The `View` has a `body` property of type `some View` (you can learn more about it in the lecture).
- The `body` property contains what is actually viewed on the Interface. In this case, it is a `VStack` (Vertical Stack), that contains an `Image` and a `Text`. No worries, you will learn more about the different components later on.
- There are also some other functions attached to it, like `.padding()` or `.imageScale(.large)`. These are _modifiers_ and we will cover them soon.

When we look at the preview, we can see a small globe icon and a text under it that says _Hello, world!_. It is vertically stacked (`VStack`), and is an `Image` and a `Text`.

There is also a second Swift file that contains the following code:

```Swift
import SwiftUI

@main
struct Demo_SwiftUI_AppApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

- This file contains the `@main` macro, which defines for the compiler, that this is the entry point of our application.
- The `struct` is inheriting from `App`, which is responsible to setup everything for us to run our app.
- Inside the `body` property, we have a `WindowGroup` which contains the call to the `ContentView` that we discussed earlier. The `WindowGroup` will create the _window_ in which our application will run.

Now that we have covered the basic starting code of our application, let's have a closer look at the declarative approach.

## SwiftUI

The main idea behind a declarative UI framework is, that you describe what should be displayed rather than how it is displayed. How the result is achieved is the responsibility of SwiftUI.

Here is a simple example: "I want to display a list to the user with the following items: SwiftUI, List, Demo". If we translate this to SwiftUI, we can do that by using `Text` elements inside a `List` element. This is the code for our example:

```Swift
List {
  Text("SwiftUI")
  Text("List")
  Text("Demo")
}
```

As you can see, we don't create views, retain their reference, etc. Instead, we describe what we want to see, a list with 3 text elements.

If we now want the first element to be larger and bold, you can use modifiers to achieve that. Again, no worries, we will cover how modifiers work soon. The following code creates a list with 3 text elements and makes the first one larger and bold:

```Swift
List {
  Text("SwiftUI")
    .font(.largeTitle)
    .bold()
  Text("List")
  Text("Demo")
}
```

Now that we have talked about the idea behind declarative UI frameworks, lets move on and learn about the different standard elements we have available.
