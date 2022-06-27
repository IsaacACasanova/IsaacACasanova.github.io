---
layout: post
title: Swift 5.3 - What's New
description: There's been a lot of great strides made with the release of Swift 5.3.  I'll go over s...
date: 2020-11-28 15:01:35 +0300
image: /images/swift.jpg
tags: [swift]
---

There's been a lot of great strides made with the release of Swift 5.3.  I'll go over some of the updates -- there's been lots of great improvements!   For full disclosure on everything that's included, refer to [the release notes](https://swift.org/blog/swift-5-3-released/).

#  Synthesized Comparable conformance for enum types

 This means that `enum` declarations automatically get `Comparable` conformance for free.   There are a few exceptions, however.  A conformance will not be synthesized if a type has raw values, non recursively-conforming associated values or an explicit `<` implementation.

 Here's an example of this update:

```swift
enum Volume {
    case low
    case medium
    case high
}

([.high, .low, .medium] as [Volume]).sorted()
// Results in [Volume.low, Volume.medium, Volume.high]
```

#  Refined didSet Semantics

A performance improving change has been made to `didSet` semantics:

If a `didSet` observer does not reference the `oldValue` in its body, then the call to fetch the `oldValue` will be skipped.

Here's an example of how these changes work:

```swift
struct Record: Equatable {
    let artistName: String
    let songName: String
}

class RecordLabel {
    var numberOfRecordsAdded: Int = 0 {
        didSet { print("didSet called") }
    }

    var records = [Record]()
    
    let maxNumberOfRecords: Int

    init(maxNumberOfRecords: Int) {
        self.maxNumberOfRecords = maxNumberOfRecords
    }

    func updateRecordCount(with newRecords: [Record]) {
        guard records.count < maxNumberOfRecords else {
            print("max number of records reached: \(maxNumberOfRecords)!")
            return
        }
        for record in newRecords {
            if !records.contains(record) {
                records.append(record)
                numberOfRecordsAdded += 1
            }
        }
    }
}

let recordLabel = RecordLabel(maxNumberOfRecords: 1000)
/// This calls the getter on 'numberOfRecordsAdded' even
/// though 'oldValue' is never referred to inside 
/// numberOfRecordsAdded's didSet
var records = [Record]()
for index in 0..<1000 {
    let record = Record(
        artistName: "artist\(index)",
        songName: "song\(index)"
    )
    records.append(record)
}
recordLabel.updateRecordCount(with: records)
```

With the improvements, now the `oldValue` in `numberOfRecordsAdded` won't be accessed, so in the case where lots of new records are added, unneccessary expensive work is avoided.

# Increase availability of implicit self in @escaping closures

There's a lot more about this [here](https://github.com/apple/swift-evolution/blob/master/proposals/0269-implicit-self-explicit-capture.md), and I encourage you to read it to get the full set of changes.

The most obvious improvement is that this error is easier to handle:

```
error: reference to property 'x' in closure requires explicit 'self.' to make capture semantics explicit
```

Say for example, we created a class like this:

```swift
class TestClass {
    func longRunningAsyncCall(work: @escaping () -> Void) {
        work()
    }
}
```

Previously, when writing a closure, you'd have to reference every usage of self explicitly, like this:

```swift
longRunningAsyncCall {
    self.performOperation()
    self.performAnotherOperation()
    self.finish()
}
```

Now, you can add `self` in the closure capture list, and drop the other references:

```swift
longRunningAsyncCall { [self] in
    performOperation()
    performAnotherOperation()
    finish()
}
```

Additionally, if the type owning the closure is a value type (like a struct or enum), then you could write the closure like this:

```swift
longRunningAsyncCall {
    performOperation()
    performAnotherOperation()
    finish()
}
```

Personally, I'd always add `[self]` in the closure capture list for consistency, but this change makes it _soo_ much cleaner when referencing self within closures. Lots of unnecessary code is made redundant.

# Multi-Pattern Catch Clauses

This update makes it possible to handle multiple error cases in the `catch` portion of a `try-catch` statement.

Previously, if you wanted to handle multiple error cases, you'd have to do the following:

```swift
do {
    try createRecord()
} catch let error as RecordCreationError {
    switch error {
        case RecordCreationError.outOfSpace(let msg),
        case RecordCreationError.invalidArtist(let msg):
        displayMessageToUser(msg)
    }
}
```

But this is awkward, and it requires a boilerplate cast down to `RecordCreationError`.

Now you can write this:

```swift
do {
    try createRecord()
} catch RecordCreationError.outOfSpace(let msg),
        RecordCreationError.invalidArtist(let msg):
        displayMessageToUser(msg)
}
```

This is much neater and easier to read than the first example, and more naturally supports Swift's extensive usage of pattern matching.

# Multiple Trailing Closures

This change makes it so that multiple labeled trailing closures can follow an initial unlabeled trailing closure.  If you've been an iOS Engineer for any period of time, you've probably come across the wonky `UIView.animate` API.

```swift
UIView.animate(withDuration: 0.3, animations: {
  self.view.alpha = 0
}, completion: { _ in
  self.view.removeFromSuperview()
})
```

Not only is this difficult to understand if you're writing it for the first time, but when working in teams that often have rules around parameter alignment and closure syntax, these blocks of code can be a nightmare to maintain.

Even though the syntax is simplified with the first trailing closure, the second closure still has to be wrapped with the right parentheses `)` before being syntactically valid. 

With the improvements to the Swift language, the above can be written like this:

```swift
UIView.animate(withDuration: 0.3) {
  self.view.alpha = 0
} completion: { _ in
  self.view.removeFromSuperview()
}
```

The syntax is much cleaner and easier to follow, and you're still able to understand the second closure is the completion handler.

# Float16 Type

A new `Float16` type has been introduced. This type is used extensively in GPU (graphics) and ML programming.

```swift
let float16Value: Float16 = 1
```

# Conclusion

These are some of the improvements made to the Swift programming language in version 5.3. There's a lot more to cover! To get the full list of changes, check [here](https://swift.org/blog/swift-5-3-released/). Let me know if these examples have been helpful to your understanding, or if you have any suggestions in the comments section. Until next update!  

