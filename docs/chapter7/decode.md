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

Let's have a look how the struct would look like.

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

​Create the data structure as Decodable structs
Use JSONDecoder to automatically transform JSON file to Swift objects

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

```Swift
// JSON: {"name": "Garrit"}

struct DataStructure: Decodable {
    let name: String
}

let decoder = JSONDecoder()
decoder.keyDecodingStrategy = .convertFromSnakeCase
let result = try? decoder.decode(DataStructure.self, from: data)
```

## Using custom CodingKeys
