---
title: Opaque and Boxed Protocol Types
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**

1. **Opaque Types란?**
2. **Opaque Types의 기본 문법**
3. **Opaque Types vs. 프로토콜 타입**
4. **Opaque Types의 주요 사용 사례**
5. **주의사항**
6. **요약**

## **Opaque Types란?**

Swift의 **Opaque Types**는 함수나 메서드가 반환하는 타입이 구체적으로 명시되지 않지만, 특정 프로토콜을 준수하는 타입임을 보장하는 방식입니다. 이는 `some` 키워드를 통해 표현됩니다.

### **핵심 특징**
1. **구체적인 타입 숨기기**: 함수나 메서드가 반환하는 실제 타입을 숨길 수 있습니다.
2. **타입 안정성 유지**: 반환된 값은 특정 프로토콜을 준수하므로, 타입 안정성을 유지합니다.
3. **유연성 제공**: 구현 세부사항을 노출하지 않고도, 호출자는 반환된 값의 동작을 예측할 수 있습니다.

---

## **Opaque Types의 기본 문법**

```swift
func someFunction() -> some Protocol {
    // 반환값은 Protocol을 준수하는 특정 타입
}
```

- `some` 키워드는 반환 타입이 특정 프로토콜을 준수하는 **하나의 구체적 타입**임을 나타냅니다.
- 호출자는 반환된 값의 실제 타입을 알 필요가 없으며, 단지 해당 프로토콜의 요구사항을 사용할 수 있습니다.

---

## **Opaque Types vs. 프로토콜 타입**

| **특징**              | **Opaque Types (`some`)**                          | **프로토콜 타입**                     |
|-----------------------|----------------------------------------------------|---------------------------------------|
| **타입 일관성**       | 항상 동일한 구체적 타입을 반환함                   | 다양한 타입을 반환할 수 있음          |
| **타입 추론 가능성**  | 컴파일러가 반환 타입을 추론할 수 있음              | 호출자가 반환 타입을 직접 관리해야 함 |
| **사용 용도**         | SwiftUI 등에서 뷰 계층 구조를 간결하게 표현         | 다형성을 활용한 유연한 설계           |

---

## **Opaque Types의 주요 사용 사례**

### 1. **SwiftUI에서 View 반환**
SwiftUI에서는 `View` 프로토콜을 준수하는 타입을 반환하는 경우가 많습니다. 이때 `some View`를 사용하여 구체적인 타입을 숨길 수 있습니다.

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
    }
}
```

- `body`는 `View` 프로토콜을 준수하는 **하나의 구체적 타입**을 반환합니다.
- 호출자는 `Text`가 반환된다는 사실을 몰라도 `View`의 메서드를 사용할 수 있습니다.

---

### 2. **다양한 타입을 반환하는 함수**
Opaque Types는 함수 내부에서 다양한 타입을 반환하면서도, 외부에서는 동일한 프로토콜을 준수하는 타입으로 처리할 수 있게 합니다.

```swift
protocol Shape {
    func draw() -> String
}

struct Circle: Shape {
    func draw() -> String {
        return "Drawing a circle"
    }
}

struct Rectangle: Shape {
    func draw() -> String {
        return "Drawing a rectangle"
    }
}

func createShape(isCircle: Bool) -> some Shape {
    if isCircle {
        return Circle()
    } else {
        return Rectangle()
    }
}

let shape = createShape(isCircle: true)
print(shape.draw()) // "Drawing a circle"
```

- `createShape` 함수는 `Shape` 프로토콜을 준수하는 타입을 반환합니다.
- 호출자는 반환된 값이 `Circle`인지 `Rectangle`인지 알 필요가 없습니다.

---

## **주의사항**
1. **단일 타입만 반환 가능**: `some` 키워드는 함수가 항상 동일한 구체적 타입을 반환해야 합니다. 서로 다른 타입을 조건에 따라 반환하는 것은 불가능합니다.
   ```swift
   func invalidFunction(condition: Bool) -> some Shape {
       if condition {
           return Circle() // Error: 두 개의 다른 타입을 반환할 수 없음
       } else {
           return Rectangle()
       }
   }
   ```
2. **프로토콜 준수 필수**: 반환된 값은 반드시 지정된 프로토콜을 준수해야 합니다.

---

## **요약**
- **Opaque Types**는 `some` 키워드를 통해 구체적인 타입을 숨기고, 특정 프로토콜을 준수하는 타입을 반환합니다.
- SwiftUI와 같은 프레임워크에서 뷰 계층 구조를 간결하게 표현하는 데 유용합니다.
- 반환 타입은 항상 동일한 구체적 타입이어야 하며, 호출자는 프로토콜의 요구사항만 사용할 수 있습니다.

