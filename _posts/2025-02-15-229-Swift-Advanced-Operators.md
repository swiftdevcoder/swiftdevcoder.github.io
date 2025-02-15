---
title: Advanced Operators
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **비트 연산자 (Bitwise Operators)**  
2. **오버플로 연산자 (Overflow Operators)**  
3. **우선순위와 결합성 (Precedence and Associativity)**  
4. **사용자 정의 연산자 (Custom Operators)**  
5. **연산자 함수 (Operator Functions)**  
6. **할당 연산자와 결합 (Assignment Operator)**

## **1. 비트 연산자 (Bitwise Operators)**
비트 연산자는 데이터의 각 비트를 직접 조작하는 데 사용됩니다. 주로 저수준 프로그래밍이나 성능 최적화가 필요한 상황에서 활용됩니다.

### **주요 비트 연산자**
- **비트 NOT (~)**: 비트 값을 반전시킵니다.
  ```swift
  let initialBits: UInt8 = 0b00001111
  let invertedBits = ~initialBits // 0b11110000
  ```

- **비트 AND (&)**: 두 비트가 모두 `1`일 때만 결과가 `1`이 됩니다.
  ```swift
  let firstBits: UInt8 = 0b00001111
  let secondBits: UInt8 = 0b00111100
  let combinedBits = firstBits & secondBits // 0b00001100
  ```

- **비트 OR (|)**: 두 비트 중 하나라도 `1`이면 결과가 `1`이 됩니다.
  ```swift
  let combinedBits = firstBits | secondBits // 0b00111111
  ```

- **비트 XOR (^)**: 두 비트가 서로 다를 때만 결과가 `1`이 됩니다.
  ```swift
  let combinedBits = firstBits ^ secondBits // 0b00110011
  ```

- **비트 시프트 연산자 (<<, >>)**: 비트를 왼쪽 또는 오른쪽으로 이동시킵니다.
  ```swift
  let shiftedBits = firstBits << 2 // 0b00111100
  ```

---

## **2. 오버플로 연산자 (Overflow Operators)**
Swift는 기본적으로 안전한 연산을 제공하며, 오버플로가 발생하면 런타임 에러를 발생시킵니다. 하지만 의도적으로 오버플로를 허용하고 싶다면, 특별한 오버플로 연산자를 사용할 수 있습니다.

### **오버플로 연산자 종류**
- **덧셈 오버플로 (&+)**: 덧셈 시 오버플로를 허용합니다.
- **뺄셈 오버플로 (&-)**: 뺄셈 시 오버플로를 허용합니다.
- **곱셈 오버플로 (&*)**: 곱셈 시 오버플로를 허용합니다.

```swift
var unsignedOverflow = UInt8.max
unsignedOverflow = unsignedOverflow &+ 1 // 0으로 돌아감 (오버플로)
```

---

## **3. 우선순위와 결합성 (Precedence and Associativity)**
연산자의 우선순위와 결합성은 표현식을 평가할 때 중요한 역할을 합니다. Swift에서는 연산자의 우선순위와 결합성을 명확히 정의하여 코드의 가독성과 안정성을 높입니다.

- **우선순위(Precedence)**: 어떤 연산자가 먼저 계산될지를 결정합니다. 예를 들어, 곱셈(`*`)은 덧셈(`+`)보다 우선순위가 높습니다.
- **결합성(Associativity)**: 동일한 우선순위를 가진 연산자가 있을 때 계산 순서를 결정합니다. 예를 들어, 덧셈(`+`)은 왼쪽 결합성을 가집니다.

```swift
let result = 5 + 4 * 3 // 곱셈이 먼저 계산됨 (결과: 17)
```

---

## **4. 사용자 정의 연산자 (Custom Operators)**
Swift에서는 새로운 연산자를 정의하거나 기존 연산자의 동작을 재정의할 수 있습니다. 이를 통해 특정 도메인에 맞는 연산자를 만들 수 있습니다.

### **사용자 정의 연산자 정의 방법**
1. 연산자 이름을 정의합니다.
2. `prefix`, `infix`, `postfix` 중 하나를 선택하여 연산자의 위치를 지정합니다.
3. 연산자의 동작을 구현합니다.

```swift
// 사용자 정의 연산자 선언
prefix operator +++

// 사용자 정의 연산자 구현
prefix func +++(value: inout Int) -> Int {
    value += 2
    return value
}

var number = 5
+++number // number는 7이 됨
```

---

## **5. 연산자 함수 (Operator Functions)**
기존 연산자를 확장하거나 사용자 정의 타입에 적용할 수 있습니다. 이를 통해 클래스, 구조체, 열거형 등에서도 연산자를 사용할 수 있습니다.

```swift
struct Vector2D {
    var x: Int
    var y: Int
}

// 벡터 덧셈 연산자 정의
func + (left: Vector2D, right: Vector2D) -> Vector2D {
    return Vector2D(x: left.x + right.x, y: left.y + right.y)
}

let vector1 = Vector2D(x: 1, y: 2)
let vector2 = Vector2D(x: 3, y: 4)
let resultVector = vector1 + vector2 // Vector2D(x: 4, y: 6)
```

---

## **6. 할당 연산자와 결합 (Assignment Operator)**
Swift의 할당 연산자(`=`)는 다른 연산자와 결합하여 사용할 수 있습니다. 예를 들어, `+=`, `-=`, `*=` 등의 복합 할당 연산자를 사용할 수 있습니다.

```swift
var score = 10
score += 5 // score는 15가 됨
```

