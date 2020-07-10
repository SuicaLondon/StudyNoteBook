# Hello Swift

## The difference of struct and class
| Struct | Table |
| ----------- | ----------- |
| Value type | Reference type |
| Copied when passed or assigned | Passed around via pointers |
| Copy on write | Automatically reference counted |
| Functional programming | Object-oriented programming |
| No inheritance | Inheritance (single) |
| "Free" init initializes All vars | "Free" init initializes NO vars |
| Mutability must be explicitly stated | Always mutable | 
| Your "go to" data structure | Used in specific circumstances |
| Everything you've seen so for is a structure (except View which is a protocol) | The ViewModel in MVVM is always a class(also, UIKit (old style iOS) is class-based)

## How to use ForEach to iterate the data of Dictionary

```Swift
ForEach(self.dectionary.map{$0}, id: \.key) { test in
  Text("\(test.name)")
}
```
