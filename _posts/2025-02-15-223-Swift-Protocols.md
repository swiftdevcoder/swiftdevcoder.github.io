---
title: 23.Protocols
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **프로토콜의 정의와 사용**   
2. **프로토콜의 주요 특징**   
3. **프로토콜의 활용 사례**   
4. **요약**

## **프로토콜(Protocols)이란?**
프로토콜은 특정 작업이나 기능을 수행하기 위해 필요한 메서드, 프로퍼티 또는 기타 요구사항들의 청사진(blueprint)을 정의합니다. 클래스, 구조체 또는 열거형은 프로토콜을 채택(adopt)하고 준수(conform)하여 이러한 요구사항들을 실제로 구현할 수 있습니다.

프로토콜은 코드의 재사용성과 유연성을 높이며, 객체 간의 상호작용을 명확히 정의하는 데 도움을 줍니다.

---

## **프로토콜의 정의와 사용**
### 1. **프로토콜 정의**
프로토콜은 `protocol` 키워드를 사용하여 정의됩니다. 예시는 다음과 같습니다:

```swift
protocol SomeProtocol {
    var someProperty: Int { get set } // 읽기/쓰기 가능한 프로퍼티
    func someMethod() -> String       // 메서드 요구사항
}
```

- **프로퍼티 요구사항**: 프로토콜은 특정 이름과 타입의 프로퍼티를 요구할 수 있습니다. `{ get }` 또는 `{ get set }`을 통해 읽기 전용 또는 읽기/쓰기 가능 여부를 지정합니다.
- **메서드 요구사항**: 프로토콜은 특정 이름과 파라미터, 반환 타입의 메서드를 요구할 수 있습니다.

---

### 2. **프로토콜 채택 및 준수**
클래스, 구조체, 열거형은 프로토콜을 채택하고 요구사항을 구현하여 프로토콜을 준수할 수 있습니다.

```swift
struct SomeStructure: SomeProtocol {
    var someProperty: Int = 0 // 프로퍼티 구현
    func someMethod() -> String {
        return "Hello, Protocol!"
    }
}
```

- 프로토콜의 모든 요구사항을 구현해야 합니다. 그렇지 않으면 컴파일 오류가 발생합니다.

---

### 3. **프로토콜 상속**
프로토콜은 다른 프로토콜을 상속받아 확장할 수 있습니다. 상속받은 프로토콜은 부모 프로토콜의 요구사항도 포함합니다.

```swift
protocol AnotherProtocol: SomeProtocol {
    func anotherMethod()
}
```

---

## **프로토콜의 주요 특징**
### 1. **프로토콜을 이용한 다형성**
프로토콜을 타입으로 사용하여 다양한 타입의 인스턴스를 동일한 방식으로 처리할 수 있습니다.

```swift
func process(value: SomeProtocol) {
    print(value.someMethod())
}

let instance = SomeStructure()
process(value: instance)
```

---

### 2. **프로토콜 조합**
여러 프로토콜을 동시에 준수해야 하는 경우 `&` 연산자를 사용하여 조합할 수 있습니다.

```swift
protocol Named {
    var name: String { get }
}

protocol Aged {
    var age: Int { get }
}

struct Person: Named, Aged {
    var name: String
    var age: Int
}

func wishHappyBirthday(to celebrator: Named & Aged) {
    print("Happy birthday, \(celebrator.name)! You're \(celebrator.age)")
}

let birthdayPerson = Person(name: "John", age: 30)
wishHappyBirthday(to: birthdayPerson)
```

---

### 3. **프로토콜 확장**
`extension` 키워드를 사용하여 프로토콜에 기본 구현을 제공할 수 있습니다. 이를 통해 프로토콜을 준수하는 모든 타입이 기본적으로 해당 기능을 사용할 수 있습니다.

```swift
extension SomeProtocol {
    func someMethod() -> String {
        return "Default Implementation"
    }
}
```

---

### 4. **프로토콜과 제네릭**
프로토콜은 제네릭과 함께 사용되어 강력한 추상화를 제공합니다. 예를 들어, 특정 프로토콜을 준수하는 타입만 제네릭 함수나 제네릭 타입에서 사용하도록 제한할 수 있습니다.

```swift
func genericFunction<T: SomeProtocol>(value: T) {
    print(value.someMethod())
}
```

---

## **프로토콜의 활용 사례**
1. **델리게이션(Delegation)**:
   - iOS 개발에서 델리게이션 패턴은 프로토콜을 기반으로 동작합니다. 예를 들어, `UITableViewDelegate`는 테이블 뷰의 동작을 위임받는 역할을 합니다.

2. **타입 지정**:
   - 컬렉션 내에서 특정 프로토콜을 준수하는 타입만 저장하거나 처리할 수 있습니다.

3. **코드 재사용성**:
   - 여러 타입에서 공통된 기능을 정의하고 구현할 수 있어 코드의 재사용성을 높입니다.

---

## **요약**
Swift의 프로토콜은 다음과 같은 핵심 개념을 제공합니다:
- **청사진 역할**: 메서드, 프로퍼티 등의 요구사항을 정의합니다.
- **다형성 지원**: 프로토콜을 타입으로 사용하여 다양한 타입을 동일한 방식으로 처리할 수 있습니다.
- **확장 가능성**: 프로토콜 확장을 통해 기본 구현을 제공할 수 있습니다.
- **유연성**: 프로토콜 조합, 상속 등을 통해 복잡한 요구사항을 표현할 수 있습니다.
