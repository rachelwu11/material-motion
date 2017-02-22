---
layout: page
title: _nextOperator
status:
  date: December 13, 2016
  is: Stable
interfacelevel: L3
implementationlevel: L4
library: reactive-motion
depends_on:
  - /starmap/specifications/observable/MotionObservable
availability:
  - platform:
    name: Android
    url: https://github.com/material-motion/streams-android
    tests_url: https://github.com/material-motion/streams-android/blob/develop/library/src/test/java/com/google/android/material/motion/streams/MotionObservableTests.java
  - platform:
    name: iOS (Swift)
    url: https://github.com/material-motion/streams-swift
    tests_url: https://github.com/material-motion/streams-swift/blob/develop/tests/unit/operator/_operatorTests.swift
  - platform:
    name: JavaScript
    url: https://github.com/material-motion/material-motion-js
    tests_url: https://github.com/material-motion/material-motion-js/blob/develop/packages/streams/src/__tests__/MotionObservable-nextOperator.test.ts
interaction:
  inputs:
    - input:
      name: upstream
      type: T
  outputs:
    - output:
      name: downstream
      type: U
---

# _nextOperator specification

This is the engineering specification for the `MotionObservable` operator: `_nextOperator`.

## Overview

`_nextOperator` is a means by which new operators can be created. An operator can change, add, or
remove values in the stream. An operator can also change the type of emitted values.

## MVP

### Expose _nextOperator API

`operation` should be a block that accepts a `T` value and a block that represents the `next`
channel.

```swift
class MotionObservable<T> {
  public func _nextOperator<U>(operation: (T, (U) -> Void) -> Void) -> MotionObservable<U>
```

### Pass next to the operation function

The operation should only be allowed to invoke `next`. Pass the observer's next function to the
operation.

```swift
class MotionObservable<T> {
  public func _nextOperator<U>(operation: (T, (U) -> Void) -> Void) -> MotionObservable<U>
    return MotionObservable<U> { observer in
      let subscription = self.subscribe(next: { value in
        operation(value, observer.next)
      }
      return {
        subscription.unsubscribe()
      }
    }
  }
}
```