# Handling data in Swift

## What is JSON?

JSON is the abbreviation for JavaScript Object Notation. And you can store different data types and collections with it. For example, arrays and dictionaries.

```JSON
{
  "category": "Science: Computers",
  "type": "multiple",
  "difficulty": "medium",
  "question": "Which of these people was NOT a founder of Apple Inc?",
  "correct_answer": "Jonathan Ive",
  "incorrect_answers": [
    "Steve Jobs",
    "Ronald Wayne",
    "Steve Wozniak"
  ]
}
```

## Parse JSON into structs

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
