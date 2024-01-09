# Binding

You can use _binding_ to create a two-way connection between a state property in one view and another view that can display and change according to the state. That means, we can keep a _single source of truth_ in a parent view, and change this value in another view, for example a subview. One example we already have seen is the `TextField`.

Let's take a look at the last example, the _Decider_ app. There is a lot going on in the view. How about we refactor the `List` and put it into its own view. This will remove not only the code to display the `List` into a new view, but also the `TextField` and therefore the `inputText` state property.

In order to use the same `DeciderModel` instance in both views (remember: _single source of truth_), we need to use `@Binding` instead of `@State` in the new `OptionListView`. To hand-over the `DeciderModel` instance as a two-way binding, we need to use the `$` in front of the variable name, to let the compiler know that this is a binding.

Let's look at the code. Here is the new `ContentView`:

```Swift
@State private var deciderModel = DeciderModel()

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
        OptionListView(deciderModel: $deciderModel)
    }
}
```

And here is the new `OptionListView`:

```Swift
@Binding var deciderModel: DeciderModel
@State private var inputText = ""

var body: some View {
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
```

Congratulations, we just have made our code more easily reusable and maintainable by splitting it up.

If you have made these changes, you will notice an error with the `Preview`. You can easily fix that by wrapping the `DeciderModel` instance in a `.constant()`. This is only needed for the preview.

```Swift
#Preview {
    OptionListView(deciderModel: .constant(DeciderModel()))
}
```

After learning about binding, next up is environment.
