# Controls in SwiftUI

In the next step, we want to make our example interactive. To be able to do this, we will use controls.

## Button

We want to turn the heart into a button and toggle the state on click. There are different ways to do this in SwiftUI and we will use a `Button`.

A `Button` has an action and a label. The label is what is displayed to the user, in our case, the image of the heart. The action is the closure that is executed, when the user clicks the button. Let's have a look at the example code:

```Swift
@State private var isLiked = false

var body: some View {
    Button(action: {
        isLiked.toggle()
    }, label: {
        Image(systemName: isLiked ? "heart.fill" : "heart")
            .foregroundStyle(.red)
    })
}
```

As you can see, we can change the state of our view and it is immidiately reflected in the view.

Let's have a look at some other controls.

## TextField

A `TextField` can be used to ask the user for text input. To use a `TextField`, we need a state property where we store the text. To use this state property, we need to _bind_ it to the `TextField`. We will check out what _binding_ is later. In simple terms, the `TextField` uses the property to store the value.

```Swift
@State private var text = ""

var body: some View {
    TextField("Enter text", text: $text)
}
```

Let's make the example a bit more interesting by adding a `Text` element that shows the text that we enter.

```Swift
@State private var text = ""

var body: some View {
    VStack {
        Text("My text: \(text)")
        TextField("Enter text", text: $text)
    }
}
```

As you can see, the text is automatically updated the moment we enter the next char.

Next, let's change the example that the text is only updated on enter. To do this, we need a second state property.

```Swift
@State private var text = ""
@State private var displayedText = ""

var body: some View {
    VStack {
        Text("My text: \(displayedText)")
        TextField("Enter text", text: $text)
            .onSubmit {
                displayedText = text
                text = ""
            }
    }
}
```

As you can see, with just a few lines of code, we can make our program interactive.

## Other controls

SwiftUI offers a lot of other controls, for example:

- Picker
- Toggle
- Link
- Slider
- Stepper
- Menu
- DatePicker

Next, we will have a look at how to use objects as states.
