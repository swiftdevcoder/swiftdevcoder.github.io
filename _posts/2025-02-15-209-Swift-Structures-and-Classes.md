---
title: Structures and Classes
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **클래스와 구조체의 정의**
2. **클래스와 구조체의 공통점**
3. **클래스와 구조체의 차이점**
4. **값 타입 vs 참조 타입**
5. **클래스의 고급 기능**
6. **구조체와 클래스의 사용 시점**


## **클래스와 구조체(Class and Structure)**

### **1. 클래스와 구조체의 정의**
- **구조체(Structure):** 값 타입(Value Type)으로 동작하며, 데이터와 관련된 메서드를 포함할 수 있습니다.
- **클래스(Class):** 참조 타입(Reference Type)으로 동작하며, 상속(Inheritance)과 같은 객체 지향 프로그래밍의 특성을 지원합니다.

#### **정의 방법**
```swift
struct SomeStructure {
    // 구조체의 속성과 메서드
}

class SomeClass {
    // 클래스의 속성과 메서드
}
```

---

### **2. 클래스와 구조체의 공통점**
클래스와 구조체는 다음과 같은 공통점을 가지고 있습니다:
1. **속성(Properties):** 값을 저장하거나 계산할 수 있습니다.
   ```swift
   struct Point {
       var x: Int
       var y: Int
   }

   class Rectangle {
       var width: Int
       var height: Int
       init(width: Int, height: Int) {
           self.width = width
           self.height = height
       }
   }
   ```

2. **메서드(Methods):** 인스턴스나 타입과 관련된 동작을 정의할 수 있습니다.
   ```swift
   struct Point {
       var x: Int
       var y: Int
       func description() -> String {
           return "Point(x: \(x), y: \(y))"
       }
   }
   ```

3. **초기화(Initializers):** 초기 상태를 설정하기 위한 생성자를 정의할 수 있습니다.
   ```swift
   struct Size {
       var width: Double
       var height: Double
       init(width: Double, height: Double) {
           self.width = width
           self.height = height
       }
   }
   ```

4. **확장(Extensions):** 기존 타입에 새로운 기능을 추가할 수 있습니다.
   ```swift
   extension Point {
       func moveBy(x deltaX: Int, y deltaY: Int) {
           x += deltaX
           y += deltaY
       }
   }
   ```

5. **프로토콜 준수(Protocol Conformance):** 특정 프로토콜을 채택하여 요구사항을 충족할 수 있습니다.
   ```swift
   protocol Drawable {
       func draw()
   }

   struct Circle: Drawable {
       func draw() {
           print("Drawing a circle")
       }
   }
   ```

---

### **3. 클래스와 구조체의 차이점**

| **특징**                | **구조체(Struct)**                           | **클래스(Class)**                          |
|-------------------------|---------------------------------------------|-------------------------------------------|
| **타입**               | 값 타입(Value Type)                        | 참조 타입(Reference Type)                 |
| **상속**               | 불가능                                     | 가능                                      |
| **디이니셜라이저**     | 없음                                       | 사용 가능(deinit)                         |
| **복사 동작**          | 복사 시 새로운 인스턴스 생성               | 참조만 전달                              |
| **변경 가능성(Mutability)** | `var`로 선언된 경우 변경 가능              | 항상 변경 가능                            |

#### **예제 코드**
```swift
// 구조체: 값 타입
struct Resolution {
    var width: Int
    var height: Int
}

let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
cinema.width = 2048 // cinema의 width만 변경됨, hd는 변경되지 않음

// 클래스: 참조 타입
class VideoMode {
    var resolution = Resolution(width: 1920, height: 1080)
    var interlaced = false
}

let someVideoMode = VideoMode()
let anotherVideoMode = someVideoMode
anotherVideoMode.interlaced = true // someVideoMode의 interlaced도 변경됨
```

---

### **4. 값 타입 vs 참조 타입**
- **값 타입(Struct):** 변수나 상수에 할당하면 데이터가 복사됩니다. 즉, 원본 데이터는 영향을 받지 않습니다.
- **참조 타입(Class):** 변수나 상수에 할당하면 참조만 전달됩니다. 따라서 한쪽에서 변경하면 다른 쪽에도 영향을 미칩니다.

#### **값 타입의 예시**
```swift
struct Point {
    var x: Int
    var y: Int
}

var point1 = Point(x: 10, y: 20)
var point2 = point1
point2.x = 30

print(point1.x) // 출력: 10 (point1은 변경되지 않음)
print(point2.x) // 출력: 30
```

#### **참조 타입의 예시**
```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

let person1 = Person(name: "Alice")
let person2 = person1
person2.name = "Bob"

print(person1.name) // 출력: Bob (person1과 person2는 동일한 인스턴스를 참조)
print(person2.name) // 출력: Bob
```

---

### **5. 클래스의 고급 기능**
1. **상속(Inheritance):** 클래스는 다른 클래스로부터 속성과 메서드를 상속받을 수 있습니다.
   ```swift
   class Animal {
       func makeSound() {
           print("Some sound")
       }
   }

   class Dog: Animal {
       override func makeSound() {
           print("Bark")
       }
   }
   ```

2. **디이니셜라이저(deinit):** 클래스 인스턴스가 해제될 때 실행되는 코드를 정의할 수 있습니다.
   ```swift
   class File {
       var name: String
       init(name: String) {
           self.name = name
       }
       deinit {
           print("\(name) is being deallocated")
       }
   }
   ```

3. **참조 카운팅:** 클래스는 자동 참조 카운팅(ARC)을 통해 메모리를 관리합니다.

---

### **6. 언제 구조체를 사용하고, 언제 클래스를 사용할까?**
- **구조체 사용 시점:**
  - 단순한 데이터 모델링이 필요한 경우.
  - 값 타입의 복사 동작이 적합한 경우.
  - 상속이 필요하지 않은 경우.

- **클래스 사용 시점:**
  - 객체 간 공유가 필요한 경우.
  - 상속을 통해 기능을 확장해야 하는 경우.
  - 디이니셜라이저가 필요한 경우.

