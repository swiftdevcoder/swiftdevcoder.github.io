---
title: 26.Automatic Reference Counting
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Automatic Reference Counting (ARC)란?**  
2. **ARC 동작 원리**  
3. **강한 참조와 순환 참조 문제**  
4. **예시 코드**  
5. **주의사항**

## **1. Automatic Reference Counting (ARC)란?**
- ARC는 Swift에서 클래스 인스턴스의 메모리를 자동으로 관리하는 시스템입니다.
- 개발자가 수동으로 메모리를 할당하거나 해제할 필요가 없습니다.
- 클래스 인스턴스가 더 이상 사용되지 않을 때, ARC는 해당 인스턴스를 자동으로 메모리에서 해제합니다.


## **2. ARC 동작 원리**
ARC는 각 클래스 인스턴스의 참조 횟수를 추적하여 메모리를 관리합니다:
1. **참조 횟수 증가**:
   - 새로운 상수, 변수 또는 프로퍼티가 특정 인스턴스를 참조하면 참조 횟수가 1 증가합니다.
2. **참조 횟수 감소**:
   - 참조하던 변수나 상수가 더 이상 해당 인스턴스를 가리키지 않으면 참조 횟수가 1 감소합니다.
3. **메모리 해제**:
   - 참조 횟수가 0이 되면 ARC는 해당 인스턴스를 메모리에서 해제하고, `deinit` 메서드(디이니셜라이저)를 호출합니다.


## **3. 강한 참조와 순환 참조 문제**
### **강한 참조 (Strong Reference)**
- 기본적으로 모든 참조는 "강한 참조"입니다.
- 강한 참조는 참조된 인스턴스가 메모리에서 해제되지 않도록 유지합니다.

### **순환 참조 (Retain Cycle)**
- 두 개 이상의 인스턴스가 서로를 강하게 참조하면, 참조 횟수가 0이 될 수 없어 메모리 누수가 발생합니다.
- 이를 해결하기 위해 **약한 참조(weak reference)** 또는 **비소유 참조(unowned reference)**를 사용합니다.

#### **약한 참조 (Weak Reference)**
- `weak` 키워드를 사용하여 선언합니다.
- 약한 참조는 참조 횟수에 영향을 주지 않습니다.
- 참조된 객체가 해제되면 `nil`이 됩니다. 따라서 반드시 옵셔널 타입으로 선언해야 합니다.

#### **비소유 참조 (Unowned Reference)**
- `unowned` 키워드를 사용하여 선언합니다.
- 비소유 참조도 참조 횟수에 영향을 주지 않습니다.
- 참조된 객체가 해제되어도 값이 `nil`로 변경되지 않으므로, 잘못된 참조로 인해 런타임 오류가 발생할 수 있습니다.
- 참조된 객체가 항상 유효하다고 보장되는 경우에만 사용합니다.

---

## **4. 예시 코드**
아래는 ARC와 관련된 간단한 예시입니다:

### **기본 ARC 동작**
```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}

var reference1: Person?
var reference2: Person?
var reference3: Person?

reference1 = Person(name: "John") // "John is being initialized"
reference2 = reference1          // 참조 횟수 증가
reference3 = reference1          // 참조 횟수 증가

reference1 = nil                 // 참조 횟수 감소
reference2 = nil                 // 참조 횟수 감소
reference3 = nil                 // 참조 횟수 0 -> "John is being deinitialized"
```

### **순환 참조 예시 및 해결**
```swift
class Person {
    let name: String
    var apartment: Apartment?
    init(name: String) { self.name = name }
    deinit { print("\(name) is being deinitialized") }
}

class Apartment {
    let unit: String
    weak var tenant: Person? // 약한 참조로 순환 참조 방지
    init(unit: String) { self.unit = unit }
    deinit { print("Apartment \(unit) is being deinitialized") }
}

var john: Person? = Person(name: "John")
var unit4A: Apartment? = Apartment(unit: "4A")

john?.apartment = unit4A
unit4A?.tenant = john

john = nil  // "John is being deinitialized"
unit4A = nil // "Apartment 4A is being deinitialized"
```

---

## **5. 주의사항**
- **클래스 전용**: ARC는 클래스 타입에만 적용됩니다. 구조체(struct)와 열거형(enum)은 값 타입이므로 ARC와 무관합니다.
- **메모리 누수 방지**: 순환 참조를 피하기 위해 적절히 `weak` 또는 `unowned`를 사용해야 합니다.
- **디버깅 도구 활용**: Xcode의 메모리 디버깅 도구(Instruments)를 통해 메모리 누수를 확인할 수 있습니다.
