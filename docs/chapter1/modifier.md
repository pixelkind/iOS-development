# Modifiers

Modifiers are used in SwiftUI to modify the look and behavior of SwiftUI elements. They can be used to add _padding_ around an element, set a _background color_ of an element, change the _font_ that is used in a `Text` element, or can be used to _resize_ an `Image`. We will have a look at the most common ones.

Modifiers bubble down the view tree... (WRITE MORE HERE)

Please keep in mind that the position of the modifier can make a large difference how it modifies your views.

## General modifiers

Background (color, behind)
Overlay
Padding
Frame

```Swift
Text("Hello Hamster!")
    .background(.orange)
```

![Screenshot](../assets/ios-background.png)

```Swift
Text("Hello Hamster!")
    .foreground(.red)
```

![Screenshot](../assets/ios-foreground.png)

```Swift
Text("Hello Hamster!")
    .background(.orange)
    .foregroundStyle(.white)
```

![Screenshot](../assets/ios-background-foreground.png)

```Swift
Text("Hello Hamster!")
    .padding()
    .background(.orange)
    .foregroundStyle(.white)
```

![Screenshot](../assets/ios-order-01.png)

## The order of the modifier is important

```Swift
Text("Hello Hamster!")
    .background(.orange)
    .foregroundStyle(.white)
    .padding()
```

![Screenshot](../assets/ios-order-02.png)

## Modifiers for texts

```Swift
Text("Hello Hamster!")
    .font(.largeTitle)
    .italic()
    .bold()
```

![Screenshot](../assets/ios-font-02.png)

## Modifiers for images

If you remember our example from earlier with the hamster in space. The image was covering the whole screen. If we want to make an image fit into the screen, we first have to make it `.resizable()` and then we can for example use `.scaledToFit()` to make sure, that it will not be larger than our screen.

```Swift
Image(.hamster)
    .resizable()
    .scaledToFit()
```

![Screenshot](../assets/ios-image-modifier.png)

You see in this example that we have to use two modifiers in a specific order, to get the desired result.

## Control modifiers

```Swift
List {
    Text("Hello")
        .swipeActions {
            Button(action: {}) {
                Label("Delete", systemImage: "trash")
            }
        }
    Text("World")
}
```

![Screenshot](../assets/ios-swipeaction-01.png)

![Screenshot](../assets/ios-swipeaction-02.png)

Now you are ready to learn about State in SwiftUI.
