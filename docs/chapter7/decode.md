# Decode JSON into structs

The task to _decode_ a _JSON_ string into a native Swift `struct` is also called parsing.

A JSON object doesn't look too different from a Swift `struct` and when the `struct` implements the `Decodable` protocol, most often, there is not much more to do, than just using it.

Do you remember the user example?

```JSON
{
  "id": 42,
  "name": "Garrit",
  "job": "Lecturer"
}
```

Let's have a look how the struct would look like. You can clearly see the similiarities.

```Swift
struct User: Decodable {
    let id: Int
    let name: String
    let job: String
}
```

To be able to decode the JSON object into a Swift object we can use the `JSONDecoder` in Swift.

```Swift
let data = """
{
  "id": 42,
  "name": "Garrit",
  "job": "Lecturer"
}
"""

let decoder = JSONDecoder()
let result = try? decoder.decode(User.self, from: data)
```

The `result` will be an _optional_ User object containing the data from the JSON object.

You can see that we use the same property names and types as in the JSON file and translate them to the Swift version.

If we look at the more complex example, the questions, we can create a struct like this.

```Swift
struct Question: Decodable {
  enum Type: String, Decodable {
    case multiple, boolean
  }
  enum Difficulty: String, Decodable {
    case easy, medium, hard
  }
  let category: String
  let type: Type
  let difficulty: Difficulty
  let question: String
  let correctAnswer: String
  let incorrectAnswers: [String]
}
```

As you notice, we can automatically transform the type and the difficulty to enums. But if we want to load it, we have to change the default setting from the `JSONDecoder`. Because the JSON uses snake_case and we are using lowerCamelCase. In order to make that work, we can use the `keyDecodingStrategy` on the decoder. This will automatically transform the keys to lowerCamelCase.

```Swift
let decoder = JSONDecoder()
decoder.keyDecodingStrategy = .convertFromSnakeCase
let result = try? decoder.decode(Question.self, from: data)
```

## Using custom CodingKeys

In case you want define your own names, you can use a `CodingKeys` enum. In this enum, you can define the key, which is your property name, and the value, which is the key in the JSON element.

```Swift
struct Feed: Codable {
    let posts: [Post]

    enum CodingKeys: String, CodingKey {
        case posts = "items"
    }
}
```

Now you are ready to load data from the internet in your iOS app.
