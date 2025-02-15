---
title: 24.Generics
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Swift Generics(제네릭)란?**
2. **제네릭의 필요성**
3. **제네릭 함수**
4. **제네릭 타입**
5. **제네릭의 확장(Extensions with Generics)**
6. **제네릭의 제약(Constraints)**
7. **제네릭의 장점**
8. **주요 용어 정리**

## **Swift Generics(제네릭)란?**

**제네릭(Generic)**은 Swift에서 코드의 재사용성을 높이고 유연성을 제공하는 중요한 기능입니다. 제네릭을 사용하면 특정 타입에 종속되지 않고 다양한 타입에서 동작할 수 있는 함수, 메서드, 클래스, 구조체 등을 작성할 수 있습니다.

예를 들어, 배열(Array)이나 딕셔너리(Dictionary)와 같은 Swift 표준 라이브러리는 제네릭을 통해 모든 데이터 타입을 처리할 수 있도록 설계되었습니다.

---

### **1. 제네릭의 필요성**
Swift에서는 타입 안전성이 중요합니다. 따라서 타입을 명확히 지정하지 않으면 컴파일 오류가 발생할 수 있습니다. 하지만 타입마다 동일한 로직을 반복적으로 작성하는 것은 비효율적입니다.

예시:
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temp = a
    a = b
    b = temp
}

func swapTwoStrings(_ a: inout String, _ b: inout String) {
    let temp = a
    a = b
    b = temp
}
```
위 예시처럼 `Int`와 `String`을 교환하는 함수를 각각 작성해야 한다면, 타입마다 함수를 새로 만들어야 합니다. 이를 해결하기 위해 제네릭을 사용할 수 있습니다.

---

### **2. 제네릭 함수**
제네릭 함수는 특정 타입에 종속되지 않고 여러 타입에서 동작할 수 있는 함수입니다. 아래는 제네릭을 사용한 예시입니다.

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}
```

- `<T>`는 제네릭 타입 매개변수를 나타냅니다. 여기서 `T`는 "Type"의 약자로, 실제 사용 시 어떤 타입이든 될 수 있습니다.
- `swapTwoValues` 함수는 `Int`, `String`, `Double` 등 다양한 타입에서 사용할 수 있습니다.

사용 예시:
```swift
var intA = 3, intB = 5
swapTwoValues(&intA, &intB)
print(intA, intB) // 출력: 5, 3

var stringA = "Hello", stringB = "World"
swapTwoValues(&stringA, &stringB)
print(stringA, stringB) // 출력: World, Hello
```

---

### **3. 제네릭 타입**
제네릭은 함수뿐만 아니라 타입(클래스, 구조체, 열거형)에서도 사용할 수 있습니다.

#### 예시: 제네릭 스택(Stack)
```swift
struct Stack<Element> {
    var items = [Element]()
    
    mutating func push(_ item: Element) {
        items.append(item)
    }
    
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
```

- `Stack`은 제네릭 타입으로, `Element`라는 제네릭 매개변수를 사용합니다.
- `Element`는 실제로 사용될 때 결정되며, 어떤 타입이든 될 수 있습니다.

사용 예시:
```swift
var intStack = Stack<Int>()
intStack.push(1)
intStack.push(2)
print(intStack.pop()) // 출력: 2

var stringStack = Stack<String>()
stringStack.push("Hello")
stringStack.push("World")
print(stringStack.pop()) // 출력: World
```

---

### **4. 제네릭의 확장(Extensions with Generics)**
제네릭 타입은 확장(Extension)을 통해 추가 기능을 제공할 수 있습니다.

예시:
```swift
extension Stack {
    var topItem: Element? {
        return items.last
    }
}
```

- `topItem`은 스택의 가장 위에 있는 항목을 반환합니다.
- 제네릭 타입인 `Element`를 그대로 사용할 수 있습니다.

사용 예시:
```swift
if let top = intStack.topItem {
    print("Top item is \(top)")
} else {
    print("Stack is empty")
}
```

---

### **5. 제네릭의 제약(Constraints)**
때로는 제네릭 타입에 특정 조건을 부여해야 할 때가 있습니다. 이를 위해 **타입 제약(Type Constraints)**을 사용할 수 있습니다.

#### 문법:
```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // ...
}
```

#### 예시: Equatable 프로토콜을 준수하는 타입만 허용
```swift
func findIndex<T: Equatable>(of valueToFind: T, in array: [T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
```

- `T: Equatable`은 `T`가 `Equatable` 프로토콜을 준수해야 함을 의미합니다.
- `Equatable`은 두 값을 비교할 수 있는 타입(예: `==` 연산자 사용 가능)을 나타냅니다.

사용 예시:
```swift
let numbers = [1, 2, 3, 4, 5]
if let index = findIndex(of: 3, in: numbers) {
    print("Found at index \(index)") // 출력: Found at index 2
}
```

---

### **6. 제네릭의 장점**
1. **코드 재사용성**: 한 번 작성한 코드를 다양한 타입에서 사용할 수 있습니다.
2. **타입 안전성**: 컴파일 시점에 타입 검사를 수행하여 오류를 방지합니다.
3. **유연성**: 다양한 타입을 지원하면서도 코드의 가독성을 유지합니다.

---

### **7. 주요 용어 정리**
- **제네릭 타입 매개변수(Generic Type Parameter)**: `<T>`와 같이 사용되는 플레이스홀더로, 실제 타입은 사용 시 결정됩니다.
- **타입 제약(Type Constraint)**: 제네릭 타입이 특정 프로토콜 또는 클래스를 준수하도록 제한하는 조건.
- **불투명 타입(Opaque Types)**: 제네릭과 관련된 개념으로, 반환 타입을 구체적으로 노출하지 않는 경우(`some` 키워드 사용).
