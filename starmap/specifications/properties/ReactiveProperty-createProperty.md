---
layout: page
status:
  date: February 19, 2017
  is: Stable
interfacelevel: L2
implementationlevel: L4
library: material-motion
depends_on:
  - /starmap/specifications/properties/ReactiveProperty
availability:
  - platform:
    name: Android
    url: https://github.com/material-motion/reactive-motion-android/blob/develop/library/src/main/java/com/google/android/reactive/motion/ReactiveProperty.java
    tests_url: https://github.com/material-motion/reactive-motion-android/blob/develop/library/src/test/java/com/google/android/reactive/motion/PropertyReactivePropertyTests.java
  - platform:
    name: JavaScript
    url: https://github.com/material-motion/material-motion-js/blob/develop/packages/streams/src/properties/ReactiveProperty.ts
    tests_url: https://github.com/material-motion/material-motion-js/blob/develop/packages/streams/src/properties/__tests__/reactiveProperty.test.ts
  - platform:
    name: iOS (Swift)
    url: https://github.com/material-motion/material-motion-swift/blob/develop/src/ReactiveProperty.swift
    tests_url: https://github.com/material-motion/material-motion-swift/blob/develop/tests/unit/ReactivePropertyTests.swift
---

# createProperty feature specification

This is the engineering specification for the `createProperty` API.

## Overview

`createProperty(withInitialValue:)` creates an **anonymous** ReactiveProperty with a given initial
value.

> For languages that don't allow top-level functions, `ReactiveProperty.of()` is the preferred API
> signature.

```swift
let someProperty = createProperty(withInitialValue: 20)
```
```java
ReactiveProperty<Float> property = ReactiveProperty.of(100f);
```

## MVP

### Expose a createProperty API

It should be genericized on type T.

```swift
public func createProperty<T>(withInitialValue initialValue: T) -> ReactiveProperty<T>
```
```java
public static <T> ReactiveProperty<T> of(T initialValue)
```

### Return a ReactiveProperty instance

```swift
func createProperty<T>(withInitialValue value: T) -> ReactiveProperty<T> {
  return ReactiveProperty(withInitialValue: value)
}
```
```java
public static <T> ReactiveProperty<T> of(T initialValue) {
  return new ValueReactiveProperty<>(initialValue);
}
```
