# State in SwiftUI

A state is a property of a view that can change over time and defines certain behaviors of the view.

As you remember, Views in SwiftUI are structs and structs are immutable. So, how can we store mutable state inside an immutable struct? To do this, SwiftUI uses _property wrappers_ to define _state_. These state-properties are handled by SwiftUI. When a value changes, the view is invalidated and recomputed. SwiftUI uses an observe-pattern to do this.

Remember: Your view state should be the _single source of truth_!

To define a state in SwiftUI, we use the `@State` property wrapper.

```Swift
@State private var isLiked = false
```

It looks like a normal variable declaration, just with the `@State` keyword in front. In this case, we declare a variable called `isLiked` that has the inital value `false`.

Next we want to have a look how we can use the state in our view:

```Swift
@State private var isLiked = false

var body: some View {
    Image(systemName: isLiked ? "heart.fill" : "heart")
        .foregroundStyle(.red)
}
```

As you can see, we are using the ternary operator to write an inline if-statement. If `isLiked` is `true`, we want to display a filled heart, otherwise, we want to show just outline of the heart.

If you change the value of isLiked to true, you will see that it will change.

Let's continue and check out how we can use controls in combination with states.
