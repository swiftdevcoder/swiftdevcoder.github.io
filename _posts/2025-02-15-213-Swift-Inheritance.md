---
title: Inheritance
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **상속(Inheritance)이란?**
2. **기본 문법**
3. **재정의(Overriding)**
4. **Super 키워드**
5. **Final 키워드**
6. **Deinitialization**
7. **상속과 관련된 주요 규칙**


## **1. 상속(Inheritance)이란?**
- **상속**은 클래스가 다른 클래스의 속성(property), 메서드(method), 기타 특성을 물려받는 메커니즘입니다.
- Swift에서는 **클래스**와 **프로토콜**에서 상속을 지원합니다. (구조체(struct)와 열거형(enum)은 상속을 지원하지 않음)
- 상속을 통해 코드의 재사용성을 높이고, 계층적 구조를 설계할 수 있습니다.

### **주요 용어**
- **슈퍼클래스(Superclass)**: 다른 클래스에게 자신의 특성을 물려주는 클래스.
- **서브클래스(Subclass)**: 슈퍼클래스로부터 특성을 물려받는 클래스.
- **재정의(Override)**: 서브클래스가 슈퍼클래스의 메서드, 프로퍼티, 또는 서브스크립트를 변경하여 사용하는 것.

---

## **2. 기본 문법**
### **클래스 상속 선언**
```swift
class 슈퍼클래스 {
    // 슈퍼클래스의 속성 및 메서드
}

class 서브클래스: 슈퍼클래스 {
    // 서브클래스의 추가 속성 및 메서드
}
```

### **예시**
```swift
class Vehicle {
    var currentSpeed = 0.0
    
    func description() -> String {
        return "현재 속도는 \(currentSpeed) km/h 입니다."
    }
}

class Bicycle: Vehicle {
    var hasBasket = false
}
```
- `Bicycle` 클래스는 `Vehicle` 클래스를 상속받아 `currentSpeed`와 `description()` 메서드를 사용할 수 있습니다.
- `Bicycle` 클래스는 자체적으로 `hasBasket`이라는 새로운 프로퍼티를 추가했습니다.

---

## **3. 재정의(Overriding)**
서브클래스는 슈퍼클래스의 메서드, 프로퍼티, 서브스크립트를 재정의하여 동작을 변경할 수 있습니다. 재정의 시에는 반드시 `override` 키워드를 사용해야 합니다.

### **메서드 재정의**
```swift
class Car: Vehicle {
    override func description() -> String {
        return "자동차의 현재 속도는 \(currentSpeed) km/h 입니다."
    }
}
```
- `Car` 클래스는 `Vehicle` 클래스의 `description()` 메서드를 재정의하여 새로운 반환값을 제공합니다.

### **프로퍼티 재정의**
#### Getter/Setter 재정의
```swift
class Car: Vehicle {
    override var currentSpeed: Double {
        willSet {
            print("속도가 \(newValue)로 변경됩니다.")
        }
    }
}
```
- `willSet`과 `didSet`을 사용하여 프로퍼티 값이 변경되기 전/후에 특정 작업을 수행할 수 있습니다.

#### 프로퍼티 감시자(Property Observer)
```swift
class Car: Vehicle {
    override var currentSpeed: Double {
        didSet {
            if currentSpeed > 100 {
                print("속도가 너무 빠릅니다!")
            }
        }
    }
}
```

---

## **4. Super 키워드**
- 서브클래스에서 슈퍼클래스의 메서드나 프로퍼티를 호출하려면 `super` 키워드를 사용합니다.
- 예: `super.description()` 또는 `super.currentSpeed`.

### **예시**
```swift
class Car: Vehicle {
    override func description() -> String {
        let superDescription = super.description()
        return "\(superDescription) (자동차)"
    }
}
```

---

## **5. Final 키워드**
- `final` 키워드를 사용하면 특정 메서드나 클래스를 더 이상 상속하거나 재정의할 수 없도록 제한할 수 있습니다.
- 예: `final class`, `final func`.

```swift
final class FinalClass {
    // 이 클래스는 상속될 수 없습니다.
}
```

---

## **6. Deinitialization**
- 클래스 인스턴스가 메모리에서 해제될 때 호출되는 `deinit` 메서드를 정의할 수 있습니다.
- 서브클래스에서 `deinit`을 정의할 경우, 슈퍼클래스의 `deinit`도 자동으로 호출됩니다.

```swift
class Vehicle {
    deinit {
        print("Vehicle 인스턴스가 해제되었습니다.")
    }
}

class Car: Vehicle {
    deinit {
        print("Car 인스턴스가 해제되었습니다.")
    }
}
```

---

## **7. 상속과 관련된 주요 규칙**
1. **클래스만 상속 가능**: Swift에서는 클래스만 상속할 수 있으며, 구조체와 열거형은 상속을 지원하지 않습니다.
2. **단일 상속**: Swift는 다중 상속을 지원하지 않습니다. 즉, 한 클래스는 단 하나의 슈퍼클래스만 가질 수 있습니다.
3. **프로토콜 다중 준수**: 클래스는 여러 프로토콜을 동시에 채택할 수 있습니다.

---

## **8. 요약**
- **상속**은 클래스 간의 계층적 관계를 형성하며, 코드 재사용성을 높이는 중요한 개념입니다.
- **재정의**를 통해 서브클래스는 슈퍼클래스의 동작을 수정하거나 확장할 수 있습니다.
- `super` 키워드를 사용하여 슈퍼클래스의 메서드나 프로퍼티에 접근할 수 있습니다.
- `final` 키워드를 사용하여 상속이나 재정의를 제한할 수 있습니다.

