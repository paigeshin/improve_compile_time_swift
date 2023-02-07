# Custom Overloaded Operator 

this can be the main reason of your slow compile time

### Wrong  

```swift

func +<A: IntegerConvertible, B: IntegerConvertible>(lhs: A, rhs: B) -> CustomNumber {
    return CustomNumber(int: lhs.int + rhs.int)
}

func addNumbers() -> CustomNumber {
    return CustomNumber(int: 1) +
           CustomNumber(int: 2) +
           CustomNumber(int: 3) +
           CustomNumber(int: 4) +
           CustomNumber(int: 5)
}

```

### Correct 

```swift
extension IntegerConvertible {
    func add<T: IntegerConvertible>(_ number: T) -> CustomNumber {
        return CustomNumber(int: int + number.int)
    }
}

func addNumbers() -> CustomNumber {
    return CustomNumber(int: 1).add(CustomNumber(int: 2))
        .add(CustomNumber(int: 3))
        .add(CustomNumber(int: 4))
        .add(CustomNumber(int: 5))
}
```

# Collection literals

Collection literals can slow your compile time. The compiler needs to do a lot of work to infer the type of those literals.

### Wrong 
```swift
extension User {
    func toJSON() -> [String : Any] 
        return [
            "firstName": firstName,
            "lastName": lastName,
            "age": age,
            "friends": friends.map   ,
            "coworkers": coworkers.map   ,
            "favorites": favorites.map   ,
            "messages": messages.map   ,
            "notes": notes.map   ,
            "tasks": tasks.map   ,
            "imageURLs": imageURLs.map   ,
            "groups": groups.map   
        ]
    }
}
```

### Correct
```swift
extension User {
    func toJSON() -> [String : Any] {
        var json = [String : Any]()
        json["firstName"] = firstName
        json["lastName"] = lastName
        json["age"] = age
        json["friends"] = friends.map   
        json["coworkers"] = coworkers.map   
        json["favorites"] = favorites.map   
        json["messages"] = messages.map   
        json["notes"] = notes.map   
        json["tasks"] = tasks.map   
        json["imageURLs"] = imageURLs.map   
        json["groups"] = groups.map   
        return json
    }
}
```
