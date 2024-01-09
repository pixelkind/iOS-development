# Observable

Once your app gets more complex, the state that you need to store will also get more complex. In this case, it makes sense to store your state in an object. By following the _single responsibility principle_, you keep your code clean and easy to maintain.

SwiftUI has the `Observation` framework and the `@Observable` macro to make that easy for us. This way, we can store multiple values in a single object and react on changes in the view.

In the next example, we will build an app that helps us make decisions called _Decider_. For example, where do we want to go for lunch, or which hoodie to wear today.

We begin with the object that will store the data. We first need to import the `Observation` framework. Next, we can begin to define our class that we prefixed with the `@Observable` macro, to let the compiler know, that we want to be able to observe this class for changes from SwiftUI. The object needs an array for storing possible options and an optional string that stores the decision, if one has been made. That's why we made it _optional_. Lastly, we want to add some functions to make it easier for us to work with it. One function to add an option, called `addOption`, one function to `reset` the list, and a function to `decide` for us.

```Swift
import Foundation
import Observation

@Observable
class DeciderModel {
    var options: [String] = []
    var selectedOption: String?

    func addOption(_ option: String) {
        options.append(option)
    }

    func reset() {
        options.removeAll()
    }

    func decide() {
        selectedOption = options.randomElement()
    }
}
```

Now, let's have a look at the view. A lot is happening here. We start with looking at the UI. We have a `VStack` with a `Text` at the top to show the selected option. Next, a `HStack` with two buttons, one to decide and one to reset. After that, we have a `List` that displays the options and a `TextField` to add new options.

```Swift
@State private var deciderModel = DeciderModel()
@State private var inputText = ""

var body: some View {
    VStack {
        Text(deciderModel.selectedOption ?? "Nothing selected")
            .font(.title)
            .padding()

        HStack(spacing: 16) {
            Button {
                deciderModel.decide()
            } label: {
                Text("Decide for me")
            }
            Button {
                deciderModel.reset()
            } label: {
                Text("Reset options")
            }
        }

        List {
            ForEach(deciderModel.options, id: \.self) { text in
                Text(text)
            }
            TextField("Add an option", text: $inputText)
                .onSubmit {
                    deciderModel.addOption(inputText)
                    inputText = ""
                }
        }
    }
}
```

As you can see in this example, we moved the logic and data storage to the `DeciderModel` class. But we leave the state property for the `inputText` in the view. Because this is view specific and might work differently, depending on our implementation.

Let's check out what _binding_ does next.
