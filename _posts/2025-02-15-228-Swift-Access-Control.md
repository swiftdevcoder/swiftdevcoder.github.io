---
title: 28.Access Control
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **접근 제어(Access Control)란?**
2. **접근 레벨(Access Levels)**
3. **접근 레벨의 규칙**
4. **접근 제어의 적용**
5. **모듈과 소스 파일**
6. **실제 사용 예시**
7. **요약**

## **접근 제어(Access Control)란?**
Swift의 접근 제어는 코드 내의 특정 선언(클래스, 구조체, 함수, 변수 등)이 어디에서 접근 가능한지를 제한하는 메커니즘입니다. 이를 통해 코드의 캡슐화를 강화하고, 의도하지 않은 외부 접근을 방지하며, 모듈 간의 명확한 경계를 설정할 수 있습니다.

---

### **접근 레벨(Access Levels)**
Swift에서는 5가지의 접근 레벨을 제공합니다. 각 레벨은 선언된 엔티티가 어디에서 접근 가능한지를 결정합니다.

1. **`open`**  
   - 가장 넓은 범위의 접근 레벨.
   - 다른 모듈에서도 접근 가능하며, 상속 및 재정의도 허용됩니다.
   - 주로 프레임워크나 라이브러리를 개발할 때 사용됩니다.

2. **`public`**  
   - `open`과 유사하게 다른 모듈에서도 접근 가능.
   - 하지만 `public`으로 선언된 클래스나 메서드는 상속이나 재정의가 불가능합니다.

3. **`internal`**  
   - 기본 접근 레벨(default).
   - 동일한 모듈 내에서만 접근 가능.
   - 별도의 접근 제어 지정자가 없는 경우 자동으로 `internal`로 설정됩니다.

4. **`fileprivate`**  
   - 선언된 파일 내에서만 접근 가능.
   - 해당 파일 내부에서만 사용해야 하는 구현 세부 사항을 숨기고 싶을 때 유용합니다.

5. **`private`**  
   - 가장 제한적인 접근 레벨.
   - 선언된 스코프(예: 클래스, 구조체, 함수) 내에서만 접근 가능.
   - 외부에서 전혀 접근할 필요가 없는 경우에 사용됩니다.

---

### **접근 레벨의 규칙**
Swift의 접근 제어는 "선언된 엔티티보다 더 넓은 범위에서 접근할 수 없다"는 원칙을 따릅니다. 즉, 어떤 타입의 접근 레벨은 그 타입을 구성하는 요소들의 접근 레벨보다 같거나 더 좁아야 합니다.

#### 예시:
```swift
public class SomeClass {
    private func someMethod() { } // private 메서드는 public 클래스 내에서만 접근 가능
}
```

---

### **접근 제어의 적용**
#### 1. **타입과 멤버**
- 타입 자체의 접근 레벨은 그 타입의 멤버(프로퍼티, 메서드 등)의 접근 레벨보다 같거나 더 넓어야 합니다.
- 예: `internal` 클래스 내부에는 `public` 메서드를 선언할 수 없습니다.

#### 2. **상속**
- 서브클래스는 슈퍼클래스와 같은 접근 레벨 또는 더 제한적인 접근 레벨을 가져야 합니다.
- `open` 클래스만 다른 모듈에서 상속될 수 있습니다.

#### 3. **프로토콜**
- 프로토콜의 요구사항은 프로토콜 자체의 접근 레벨보다 같거나 더 제한적이어야 합니다.

#### 4. **익스텐션**
- 익스텐션은 확장하려는 타입의 접근 레벨을 따릅니다.
- 특정 파일 내에서만 사용되는 익스텐션은 `fileprivate` 또는 `private`으로 제한할 수 있습니다.

---

### **모듈과 소스 파일**
- **모듈(Module)**: 하나의 패키지 단위로, 애플리케이션 또는 프레임워크로 배포됩니다.
- **소스 파일(Source File)**: 모듈 내의 개별 `.swift` 파일.
- 접근 제어는 모듈과 소스 파일의 경계를 기준으로 동작합니다.

---

### **실제 사용 예시**
```swift
// internal (기본값)
class MyClass {
    private var secretValue = 42

    func getSecretValue() -> Int {
        return secretValue
    }
}

// public 클래스
public class PublicClass {
    fileprivate var restrictedValue = 100

    func getRestrictedValue() -> Int {
        return restrictedValue
    }
}

// open 클래스
open class OpenClass {
    open func openMethod() { }
    public func publicMethod() { }
}
```

---

### **요약**
- **접근 제어**는 코드의 캡슐화와 모듈 간의 경계를 설정하는 중요한 도구입니다.
- **접근 레벨**: `open`, `public`, `internal`, `fileprivate`, `private`.
- **기본 접근 레벨**: `internal`.
- **규칙**: 선언된 엔티티보다 더 넓은 범위에서 접근할 수 없습니다.
