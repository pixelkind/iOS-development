# Loading data

After learning about concurrency in Swift, let's check out how we can actually use it to load data from the internet.

```Swift
@MainActor
func fetchData() async {
    self.storeMyData = try? await loadData()
}

private func loadData() async throws -> Data? {
    if let url = URL(string: "https://opentdb.com/api.php?amount=\(amountOfQuestions)&type=multiple") {
        let (data, _) = try await URLSession.shared.data(from: url)
        print(String(data: data, encoding: .utf8))
        return data
    } else {
        return nil
    }
}
```

```Swift
func fetchData() {
    Task.init {
        self.storeMyData = try? await loadData()
    }
}

private func loadData() async throws -> Data? {
    if let url = URL(string: "https://opentdb.com/api.php?amount=\(amountOfQuestions)&type=multiple") {
        let (data, _) = try await URLSession.shared.data(from: url)
        print(String(data: data, encoding: .utf8))
        return data
    } else {
        return nil
    }
}
```

Besides the structured concurrency approach, we can also use other approaches. Please note that I expect you to use async await in your assignments and projects.

## Loading data using combine

[Combine](https://developer.apple.com/documentation/combine) is a framework to provide a declarative API for Swift to process values over time. That includes asynchronous events, like loading data. It follows the Publisher-Subscriber pattern.

1. Want to get the data from the url
2. check if the status code is ok
3. receive the data on the main queue
4. use the data (for example assign to a view)

```Swift
cancellable = URLSession.shared
    .dataTaskPublisher(for: url)
    .tryMap { element -> Data in
        guard let httpResponse = element.response as? HTTPURLResponse, httpResponse.statusCode == 200 else {
            throw URLError(.badServerResponse)
        }
        return element.data
    }
    .receive(on: DispatchQueue.main)
    .sink { completion in
        print(completion)
    } receiveValue: { data in
        print(String(data: data, encoding: .utf8))
    }
```

## Loading data using a callback handler

```Swift
let task = URLSession.shared.dataTask(with: url) { (data, response, error) in
    guard let data = data else {
        print(error)
        return
    }
    print(String(data: data, encoding: .utf8))
    DispatchQueue.main.async {
        // return the result to the main queue
    }
}
task.resume()
```
