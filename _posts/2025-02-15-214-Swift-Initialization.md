---
title: Initialization
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **초기화(Initialization)란?**
2. **초기화의 기본 규칙**
3. **이니셜라이저의 종류**
4. **클래스 상속과 초기화**
5. **실패 가능한 이니셜라이저(Failable Initializer)**
6. **필수 이니셜라이저(Required Initializer)**
7. **Deinitialization (역초기화)**
8. **핵심 포인트 요약**


## **초기화(Initialization)란?**
초기화는 클래스, 구조체 또는 열거형의 새 인스턴스를 준비하는 과정입니다. 초기화를 통해 저장 프로퍼티에 초기값을 설정하거나, 인스턴스 사용 전 필요한 설정 작업을 수행할 수 있습니다.

Swift에서는 초기화를 위해 **이니셜라이저(initializer)**라는 특별한 메서드를 사용합니다. 이니셜라이저는 `init` 키워드로 정의됩니다.

---

## **초기화의 기본 규칙**
1. **저장 프로퍼티 초기화 필수**  
   모든 저장 프로퍼티는 초기화가 끝날 때까지 반드시 값을 가져야 합니다. 이를 위해:
   - 저장 프로퍼티에 기본값을 할당하거나,
   - 이니셜라이저에서 명시적으로 값을 설정해야 합니다.

2. **옵셔널(Optional) 프로퍼티**  
   옵셔널 타입의 프로퍼티는 초기화 시 기본값을 할당하지 않아도 됩니다. 자동으로 `nil`로 초기화됩니다.

3. **지연 저장 프로퍼티(Lazy Stored Property)**  
   `lazy` 키워드를 사용한 프로퍼티는 초기화 시점에 값을 할당하지 않고, 처음 접근할 때 초기화됩니다.

---

## **이니셜라이저의 종류**
### 1. **디자인 이니셜라이저(Designated Initializer)**
- 클래스의 주요 이니셜라이저입니다.
- 모든 저장 프로퍼티를 초기화하며, 클래스의 전체 초기화 과정을 담당합니다.
- 클래스에는 하나 이상의 디자인 이니셜라이저가 있을 수 있습니다.

```swift
class Person {
    var name: String
    var age: Int

    // 디자인 이니셜라이저
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}
```

### 2. **편의 이니셜라이저(Convenience Initializer)**
- 보조적인 역할을 하며, 디자인 이니셜라이저를 호출하여 간단히 초기화를 완료합니다.
- `convenience` 키워드로 선언합니다.

```swift
class Person {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    // 편의 이니셜라이저
    convenience init(name: String) {
        self.init(name: name, age: 0)
    }
}
```

### 3. **구조체 멤버와이즈 이니셜라이저(Memberwise Initializer)**
- 구조체는 자동으로 멤버와이즈 이니셜라이저를 제공합니다.
- 저장 프로퍼티 이름을 매개변수로 받아 초기화를 수행합니다.

```swift
struct Point {
    var x: Double
    var y: Double
}

// 자동으로 제공되는 멤버와이즈 이니셜라이저
let point = Point(x: 3.0, y: 4.0)
```

---

## **클래스 상속과 초기화**
클래스는 상속 관계에서 초기화 규칙을 따라야 합니다.

### 1. **디자인 이니셜라이저 상속**
- 서브클래스는 슈퍼클래스의 디자인 이니셜라이저를 상속받을 수 있습니다.
- 서브클래스에서 새로운 저장 프로퍼티를 추가하면, 이를 초기화해야 합니다.

```swift
class Vehicle {
    var numberOfWheels = 0
}

class Bicycle: Vehicle {
    override init() {
        super.init()
        numberOfWheels = 2
    }
}
```

### 2. **자동 상속 규칙**
- 서브클래스가 추가 이니셜라이저를 정의하지 않으면, 슈퍼클래스의 디자인 이니셜라이저와 편의 이니셜라이저를 자동으로 상속받습니다.

---

## **실패 가능한 이니셜라이저(Failable Initializer)**
- 초기화 과정에서 실패 가능성을 표현하기 위해 사용합니다.
- `init?` 키워드로 정의하며, 실패 시 `nil`을 반환합니다.

```swift
struct Animal {
    let species: String

    init?(species: String) {
        if species.isEmpty {
            return nil
        }
        self.species = species
    }
}

let animal = Animal(species: "") // nil
```

---

## **필수 이니셜라이저(Required Initializer)**
- 서브클래스에서 반드시 구현해야 하는 이니셜라이저입니다.
- `required` 키워드로 표시합니다.

```swift
class Shape {
    required init() {
        // 공통 초기화 로직
    }
}

class Circle: Shape {
    required init() {
        super.init()
        // 추가 초기화 로직
    }
}
```

---

## **Deinitialization (역초기화)**
- 클래스 인스턴스가 메모리에서 해제되기 직전에 호출되는 `deinit` 메서드를 정의할 수 있습니다.
- 주로 리소스 정리 작업에 사용됩니다.

```swift
class File {
    var filename: String

    init(filename: String) {
        self.filename = filename
    }

    deinit {
        print("\(filename) 파일이 닫혔습니다.")
    }
}
```

---

## **핵심 포인트 요약**
1. **초기화는 모든 저장 프로퍼티를 초기화하는 과정이다.**
2. **디자인 이니셜라이저와 편의 이니셜라이저는 각각 주요 및 보조 초기화를 담당한다.**
3. **상속 관계에서는 슈퍼클래스의 초기화 규칙을 따라야 한다.**
4. **실패 가능한 이니셜라이저(`init?`)는 초기화 실패 시 `nil`을 반환한다.**
5. **`deinit`은 인스턴스가 메모리에서 해제될 때 호출된다.**
