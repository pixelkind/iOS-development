# Swift

Here is a video, walking you through the basics of Swift. If you want to read instead, you can just scroll down.

<iframe id="kaltura_player" src="https://api.kaltura.nordu.net/p/324/sp/32400/embedIframeJs/uiconf_id/23450106/partner_id/324?iframeembed=true&playerId=kaltura_player&entry_id=0_r7zge69w&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;flashvars[hotspots.plugin]=1&amp;flashvars[Kaltura.addCrossoriginToIframe]=true&amp;&wid=0_tzo6y68r" width="608" height="402" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" sandbox="allow-downloads allow-forms allow-same-origin allow-scripts allow-top-navigation allow-pointer-lock allow-popups allow-modals allow-orientation-lock allow-popups-to-escape-sandbox allow-presentation allow-top-navigation-by-user-activation" frameborder="0" title="iOS Development - Introduction to Swift"></iframe>

You can find more details about Swift on the official homepage [www.swift.org](https://www.swift.org).

## Basics

### Comments

As in most other programming languages, you can write comments in Swift. Single line comments start with `//`.

```Swift
// This is a single line comment
```

While multiline comments starts with `/*` and end with `*/`.

```Swift
/* This is a
   multiline comment */
```

### Variables

If a variable is _immutable_, you can use the `let` keyword to define it.

```Swift
let name = "Garrit"
```

If you want to be able to change it, you should use the `var` keyword.

```Swift
var country = "Germany"
country = "Sweden"
```

### No semicolons

You might have noticed, that in Swift, you don't use `;` at the end of a line.

### Type inference

If you define a variable in Swift, its type is inferred from its value. Means, if you write `let name = "Garrit"`, Swift knows that the variable `name` is of type `String`.

The following two lines are doing the same thing, but the first line is the preferred way of writing it.

```Swift
let name = "Garrit"
let name: String = "Garrit"
```

And of course, it is not only true for `String`, but also for all other types, for example `Int`.

```Swift
let age = 37
let age: Int = 37
```

Sometimes, Swift cannot infer the type. In this case, you have to write it.

### Basic types

The basic types in Swift are `Int`, `Float`, `Double`, `String`, and `Bool`.

```Swift
let integer: Int = 42
let float: Float = 4.2
let double: Double = 4.2
let string: String = "Swift"
let bool: Bool = true
```

### Naming conventions

When you write Swift code, you should follow the official naming conventions. The most important are:

- Use UpperCamelCase for types and protocols
- Everything else is lowerCamelCase
- Clarity over brevity
- Avoid abbreviations

You can find more infos in the [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/).

### Operators

Some often used operators in Swift are `+`, `-`, `*`, `/`, and `%`.

```Swift
1+2		    // equals 3
5-3		    // equals 2
3*3		    // equals 9
9.0 / 3.0	// equals 3.0
9 % 4		  // equals 1
```

Note, that if you want to write a negative numbers, you don't put a space between the number and the operator.

```Swift
-3		    // equals -3
```

### Compound assingment operators

Swift has also compound assignment operators, like `+=` and `-=`. You can use them like this:

```Swift
var a = 1
a += 4      // equals 5
a -= 3      // equals 2
```

Note, that there is no `++` or `--` operator in Swift.

### Comparison operators

If you want to compare values in Swift, you can use the default comparison operators, like `==`, `!=`, etc.

```Swift
3 == 3
3 != 1
3 > 1
1 < 3
3 >= 3
1 <= 3
```

### Ternary conditional operator

In Swift and especially in SwiftUI we often use the ternary conditional operator to write a shorthand if-statement. Consider the following example:

```Swift
var wasSuccessful = false
if (statusCode < 400) {
    wasSuccessful = true
}
```

In Swift, you will often write it using the `?` and the `:` operator, while the first part after the `?` is the if-clause, while the part after the `:` is the else part of the conditional statement.

```Swift
let wasSuccessful = statusCode < 400 ? true : false
```

### String operations

If you want to insert something into a `String` in Swift, you can use the `+` operator to concatenate two strins, or you can use `\(variableName)` syntax to put a value into a `String`.

```Swift
let name = "Garrit"
let welcome = "Welcome \(name)!"
```

If you want to write a longer `String`, you can use the multiline operator `"""`.

```Swift
let multilineString = """
Here you can
write a "multiline"
string...
"""
```

## Collection Types

### Arrays

```Swift
let array = [42, 13]

var attendees = [String]()
var attendees: [String] = []
var attendees = ["Jasmin", "Anders"]

attendees.append("Garrit")
print("Number of attendees: \(attendees.count)")
```

```Swift
var emojis = ["🥚", "🐓"]
emojis.sort()

let emojis = ["🥚", "🐓"]
let sortedEmojis = emojis.sorted()
```

### Sets

```Swift
let data = Set<Int>()
let data: Set<Int> = [42, 13]
```

### Dictionaries

```Swift
let dict: [String: String] = [:]
let dict = ["key": "value"]
```

## Control flow

### If statement

```Swift
let numberOfKanelbullar = 3

if numberOfKanelbullar < 2 {
  print("We need more Kanelbullar!")
}
```

```Swift
let numberOfKanelbullar = 3

if numberOfKanelbullar < 2 {
  print("We need more Kanelbullar!")
} else {
  print("Let's have some fika!")
}
```

```Swift
let numberOfKanelbullar = 3

if numberOfKanelbullar < 2 {
  print("We need more Kanelbullar!")
} else if numbersOfKanelbullar > 10 {
  print("Let's invite more people for fika!")
} else {
  print("Let's have some fika!")
}
```

### Guard statement

```Swift
guard statusCode < 400 else {
  return
}
```

### Switch statement

```Swift
var emoji = "🐹"

switch emoji {
  case "🐹":
    print("Hamster")
  case "🦆":
    print("Duck")
  default:
    print("I don't know")
}
```

### For loops

```Swift
for index in 1...42 { // 0..<42
    print(index)
}
```

#### For loops with arrays

```Swift
let emojis = ["🐹", "🥳", "🍰", "🦆"]

for emoji in emojis {
    print(emoji)
}
```

#### For loops with dictionaries

```Swift
let emojis =
  ["hamster": "🐹", "party": "🥳", "cake": "🍰", "duck": "🦆"]

for (name, emoji) in emojis {
    print("\(emoji) is called \(name)")
}
```

### While loops

```Swift
var count = 0
while count < 3 {
    print(count)
    count += 1
}
```

### Repeat-while loops

```Swift
var count = 0
repeat {
    print(count)
    count += 1
} while count < 3
```

## Optionals

```Swift
var cat: String?

cat = "🐈"
print(cat)

if let cat {
    print(cat)
}
```

```Swift
var cat: String?

let myCat = cat ?? "🐱"
```

## Functions

```Swift
func helloWorld() {
    print("Hello World")
}
```

#### Parameter naming

```Swift
func greet(person: String) {
    print("Hello \(person)")
}
greet(person: "Jasmin")

func greetPerson(_ person: String) {
    print("Hello \(person)")
}
greetPerson("Jasmin")

func greet(person personName: String) {
    print("Hello \(personName)")
}
greet(person: "Jasmin")
```

#### Default values for parameters

```Swift
func greet(person: String = "Groot") {
    print("Hello \(person)")
}
greet() // will print "Hello Groot"
```

#### inout parameters

```Swift
func add(value: Int, toNumber internalNumber: inout Int) {
    number += value
}

var number = 32
add(value: 10, toNumber: &number)
print(number)
```

#### Returns

```Swift
func bestEmoji() -> String {
    // do something here to get the best one
    return "😱"
}

// special case for single line functions
func bestEmoji() -> String {
    "😱"
}
```

## Closures

> Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages.

> Closures can capture and store references to any constants and variables from the context in which they’re defined. This is known as closing over those constants and variables. Swift handles all of the memory management of capturing for you.

> A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns. When you declare a function that takes a closure as one of its parameters, you can write @escaping before the parameter’s type to indicate that the closure is allowed to escape.

```Swift
let emojis = ["🐹", "🥳", "🍰", "🦆"]
let result = emojis.filter { (emoji) -> Bool in
    if emoji == "🐹" {
        return true
    }
    return false
}

let resultSingleLine = emojis.filter { $0 == "🐹" }
```

If you don't want to use the parameter, you can ignore it by using the `_` instead of a parameter name.

```Swift
let emojis = ["🐹", "🥳", "🍰", "🦆"]
let result = emojis.filter { (_) -> Bool in
    false
}
```

## Classes

Classes are a reference-type. A class can inherit from another class. You can define properties, methods, subscripts, initializers, and deinitializers in a class. Classes can be _extended_, and they can conform to _protocols_.

```Swift
class Animal {
    let name: String
    let emoji: String

    init(name: String, emoji: String) {
        self.name = name
        self.emoji = emoji
    }

    func greet() {
        print("Hello \(name)!")
    }
}

let hamster = Animal(name: "Klaus", emoji: "🐹")
hamster.greet()
```

#### Property listener

```Swift
class Animal {
    let name: String
    var age: Int {
        didSet {
            print("Happy Birthday \(name) 🥳")
        }
    }

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}

let hamster = Animal(name: "Klaus", age: 1)
hamster.age += 1
```

#### Computed properties

```Swift
class Animal {
    let name: String
    var age: Int
    var info: String {
        "\(name) is \(age) years old"
    }

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}

let hamster = Animal(name: "Klaus", age: 1)
print(hamster.info)
```

#### Inheritance

```Swift
class Dog: Animal {
    func bark() {
        print("Bark!")
    }
}
```

## Structs

Structs are a value-type. You can define properties, methods, subscripts, and initializers in a struct. Structs can be _extended_, and they can conform to _protocols_.

```Swift
struct Animal {
    let name: String
    let emoji: String

    func greet() {
        print("Hello \(name)!")
    }
}

let hamster = Animal(name: "Klaus", emoji: "🐹")
hamster.greet()
```

You should prefer structs over classes, if possible.

## Enums

```Swift
enum Animal {
    case hamster, cat, dog
}

enum Animal: String {
    case hamster, cat, dog
}

enum Animal: String {
    case hamster = "🐹"
    case cat = "🐱"
    case dog = "🐶"
}
```

```Swift
enum Animal {
    case hamster, cat, dog
}

let animal = Animal.hamster // let animal: Animal = .hamster
switch animal {
case .hamster:
    print("🐹")
case .cat:
    print("🐱")
case .dog:
    print("🐶")
}
```

```Swift
enum Animal {
    case cat(String), dog(String)
}

let someAnimal = Animal.cat("Findus")
switch someAnimal {
case .cat(let name):
    print("The cat's name is \(name)")
case .dog(let name):
    print("The dog's name is \(name)")
}
```

## Protocols

```Swift
protocol Animal {
    var name: String {get}
}

struct Cat: Animal {
    var name: String
}

class Dog: Animal {
    var name: String

    init(name: String) {
        self.name = name
    }
}
```

## Extensions

You can extend an existing class or struct and confirm to a new protocol. Extensions work app-wide. For example, you can extend the `String` class.

```Swift
struct Cat {
    var name: String
}

extension Cat {
    func greet() {
        print("Hello \(name)")
    }
}
```

## Generics

```Swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var a = 42
var b = 13

swapTwoValues(&a, &b)
print(a, b)
```
