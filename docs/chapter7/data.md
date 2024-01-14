# Handling external data in Swift

If we are loading data from an external resource, we usually use data serialized into a specific format. Nowadays, that is often _JSON_.

## What is JSON?

JSON is the abbreviation for _JavaScript Object Notation_. And you can store different data types and collections with it. For example, strings, numbers, bools, arrays and dictionaries.

Let's have a look at a simple example:

```JSON
{
  "name": "Garrit"
}
```

This is a very simple object that has a single property called `name` of type `String`.

Let's add some more properties:

```JSON
{
  "id": 42,
  "name": "Garrit",
  "job": "Lecturer"
}
```

In this example, we have an object that represents a simple user. It has an `id`, a `name`, and a `job`. The `id` is a number, probably an `Int`, and the other properties are of type `String`.

Let's have a look at a bit more complex _JSON_ object:

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

As you can see, this object has the properties _category_, _type_, _difficulty_, _question_, _correct_answer_, and _incorrect_answer_. As you can probably notice, it is the data of a single question for a quiz, represented in the _JSON_ format. Besides a lot of strings, it also includes an array with strings.

Now that we have an idea what _JSON_ is and what it represents, let's have a look how we can _decode_ it into a native object in Swift.
