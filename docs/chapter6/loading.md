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
    Task {
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

[Combine](https://developer.apple.com/documentation/combine) is a framework to provide a declarative API for Swift to process values over time. That includes asynchronous events, like loading data. It follows the Publisher-Subscriber pattern. For loading data, we can use the `dataTaskPublisher` on a `URLSession` like this. You can see that after mapping the data we switch the thread on which the code will be executed.

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

## Loading data using a completion handler

If you want to load data using an `URLSession`, you can also use a completion handler. This is not the recommended way any longer. But here is an usage example:

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

Please don't forget to call `task.resume()` to start the loading operation.
