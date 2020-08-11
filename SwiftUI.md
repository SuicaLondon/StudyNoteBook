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

## Set the background color 
```
ZStack(alignment: .top) {
    Rectangle()
       .foregroundColor(Color.black)
       .edgesIgnoringSafeArea(.top)
    HStack(alignment: .center) {
        // content                 
    }
}
```

## Clear the space on the left of DatePicker
```
DatePicker("", selection:  self.$time, in: ...Date(), displayedComponents: [.hourAndMinute, .date])
.labelsHidden()
```

## Solve the problem of unclickable Spacer() in HStack
```
HStack {
    XXXX
    Spacer()
    XXXX
}
.contentShape(Rectangle())
.onTapGesture {
    XXX
}
```

## Meet a bug that the actionSheet can not update its showing state when its button was added dynatically 
It is necessary to use other sheet to replace it because when the button was clicked, the state will start from false
