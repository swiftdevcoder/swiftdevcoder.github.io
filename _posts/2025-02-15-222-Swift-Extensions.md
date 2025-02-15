---
title: 22.Extensions
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Extensions란?**
2. **Extensions의 기본 문법**
3. **Extensions로 추가할 수 있는 기능**   
4. **Extensions의 제한 사항**
5. **Extensions 활용 예시**
   


### **1. Extensions란?**
- **Extensions**는 기존 타입(클래스, 구조체, 열거형, 프로토콜 등)에 새로운 기능을 추가할 수 있는 기능입니다.
- 이미 존재하는 타입에 대해 수정 없이도 기능을 확장할 수 있습니다.
- 주요 용도:
  - 새로운 메서드 추가
  - 새로운 초기화 메서드(computed properties 포함)
  - 프로토콜 채택 및 구현
  - 중첩 타입 추가

> **주의**: Extensions를 통해 저장 프로퍼티(stored properties)를 추가할 수는 없습니다.

---

### **2. Extensions의 기본 문법**

```swift
extension SomeType {
    // 새로운 기능 추가
}
```

예시:
```swift
extension Int {
    func squared() -> Int {
        return self * self
    }
}

let number = 5
print(number.squared()) // 출력: 25
```

---

### **3. Extensions로 추가할 수 있는 기능**

#### **(1) Computed Properties**
- 저장 프로퍼티는 추가할 수 없지만, **계산된 프로퍼티(computed properties)**는 추가 가능합니다.

```swift
extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
}

let distance = 25.4
print(distance.km) // 출력: 25400.0
print(distance.cm) // 출력: 0.254
```

---

#### **(2) Instance Methods와 Type Methods**
- 인스턴스 메서드와 타입 메서드를 추가할 수 있습니다.

```swift
extension String {
    func shout() -> String {
        return self.uppercased() + "!"
    }
    
    static func greet() -> String {
        return "Hello, World!"
    }
}

let greeting = "hello".shout()
print(greeting) // 출력: "HELLO!"

print(String.greet()) // 출력: "Hello, World!"
```

---

#### **(3) Initializers**
- 새로운 초기화 메서드를 추가할 수 있습니다.
- 특히 외부 라이브러리나 시스템 타입에 커스텀 초기화 메서드를 추가할 때 유용합니다.

```swift
struct Size {
    var width = 0.0, height = 0.0
}

extension Size {
    init(value: Double) {
        self.width = value
        self.height = value
    }
}

let customSize = Size(value: 10.0)
print(customSize.width, customSize.height) // 출력: 10.0 10.0
```

---

#### **(4) Subscripts**
- 서브스크립트(subscript)를 추가하여 타입에 대한 접근 방식을 확장할 수 있습니다.

```swift
extension String {
    subscript(index: Int) -> Character? {
        guard index >= 0 && index < self.count else { return nil }
        return self[self.index(self.startIndex, offsetBy: index)]
    }
}

let text = "Swift"
print(text[2]) // 출력: Optional("i")
```

---

#### **(5) Nested Types**
- 중첩 타입(nested types)을 추가할 수 있습니다.

```swift
extension Int {
    enum Kind {
        case negative, zero, positive
    }
    
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
}

let number = -5
print(number.kind) // 출력: negative
```

---

#### **(6) Protocol Conformance**
- Extensions를 사용하여 기존 타입이 특정 프로토콜을 준수하도록 만들 수 있습니다.

```swift
protocol TextRepresentable {
    var textualDescription: String { get }
}

extension Int: TextRepresentable {
    var textualDescription: String {
        return "The number \(self)"
    }
}

let value = 42
print(value.textualDescription) // 출력: "The number 42"
```

---

### **4. Extensions의 제한 사항**
- **저장 프로퍼티 추가 불가**: Extensions에서는 저장 프로퍼티를 추가할 수 없습니다.
- **기존 메서드 재정의 불가**: Extensions로 기존 메서드를 재정의할 수 없습니다.
- **새로운 designated initializers 추가 불가**: Convenience initializer만 추가할 수 있습니다.

---

### **5. Extensions 활용 예시**

#### **(1) UIKit 확장**
UIKit의 `UIView` 클래스에 편리한 메서드를 추가할 수 있습니다.

```swift
import UIKit

extension UIView {
    func addBorder(color: UIColor, width: CGFloat) {
        self.layer.borderColor = color.cgColor
        self.layer.borderWidth = width
    }
}

let view = UIView()
view.addBorder(color: .red, width: 2.0)
```

#### **(2) Custom Operators**
Extensions를 통해 커스텀 연산자를 정의할 수도 있습니다.

```swift
extension Int {
    static func ** (base: Int, power: Int) -> Int {
        return Int(pow(Double(base), Double(power)))
    }
}

let result = 2 ** 3
print(result) // 출력: 8
```

---

### **6. 요약**
- Extensions는 기존 타입에 새로운 기능을 추가하거나 프로토콜 준수를 구현하는 데 유용합니다.
- 주요 기능:
  - Computed Properties
  - Methods (Instance & Type)
  - Initializers
  - Subscripts
  - Nested Types
  - Protocol Conformance
- 제한 사항:
  - 저장 프로퍼티 추가 불가
  - 기존 메서드 재정의 불가

