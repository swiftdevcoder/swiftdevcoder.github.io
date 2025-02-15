---
title: Methods
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Instance Methods (인스턴스 메서드)**
2. **Type Methods (타입 메서드)**
3. **Mutating Methods (변경 가능한 메서드)**
4. **Self Property**
5. **Methods in Enumerations and Structures (열거형과 구조체의 메서드)**
6. **Key Points to Remember (핵심 요약)**

## **1. Instance Methods (인스턴스 메서드)**

- **정의**: 특정 타입의 인스턴스에서 호출되는 메서드입니다.
- **특징**:
  - `func` 키워드를 사용하여 정의합니다.
  - 인스턴스 속성 및 기타 인스턴스 메서드에 접근 가능합니다.
  - `self` 키워드를 통해 현재 인스턴스를 참조할 수 있습니다.
- **예시**:
  ```swift
  struct Counter {
      var count = 0
      
      func increment() {
          self.count += 1 // self를 사용하여 인스턴스 속성 접근
      }
      
      func reset() {
          count = 0
      }
  }

  var counter = Counter()
  counter.increment()
  print(counter.count) // 출력: 1
  ```

---

## **2. Type Methods (타입 메서드)**

- **정의**: 특정 타입 자체에서 호출되는 메서드입니다.
- **특징**:
  - `static` 키워드를 사용하여 정의합니다.
  - 클래스에서는 `class` 키워드를 사용할 수도 있습니다.
  - 인스턴스 속성에는 접근할 수 없으며, 타입 속성만 사용 가능합니다.
- **예시**:
  ```swift
  struct MathUtility {
      static func add(_ a: Int, _ b: Int) -> Int {
          return a + b
      }
  }

  let result = MathUtility.add(5, 3)
  print(result) // 출력: 8
  ```

---

## **3. Mutating Methods (변경 가능한 메서드)**

- **정의**: 구조체(struct)나 열거형(enum)의 인스턴스 속성을 변경하는 메서드입니다.
- **특징**:
  - `mutating` 키워드를 사용하여 정의합니다.
  - 클래스(class)에서는 필요하지 않습니다(클래스는 기본적으로 변경 가능).
- **예시**:
  ```swift
  struct Point {
      var x = 0.0, y = 0.0
      
      mutating func moveBy(x deltaX: Double, y deltaY: Double) {
          x += deltaX
          y += deltaY
      }
  }

  var point = Point(x: 1.0, y: 1.0)
  point.moveBy(x: 2.0, y: 3.0)
  print("(\(point.x), \(point.y))") // 출력: (3.0, 4.0)
  ```

---

## **4. Self Property**

- **정의**: 모든 인스턴스 메서드는 암시적으로 `self` 프로퍼티를 가지고 있습니다.
- **사용 사례**:
  - 메서드 내에서 현재 인스턴스를 참조하거나 반환할 때 사용합니다.
  - 이름 충돌이 발생할 경우 명확히 구분하기 위해 사용됩니다.
- **예시**:
  ```swift
  struct Person {
      var name: String
      
      func getSelf() -> Self {
          return self // 현재 인스턴스 반환
      }
  }

  let person = Person(name: "John")
  let samePerson = person.getSelf()
  print(samePerson.name) // 출력: John
  ```

---

## **5. Methods in Enumerations and Structures**

- **열거형과 구조체에서도 메서드를 정의할 수 있습니다.**
- **예시**:
  ```swift
  enum TriStateSwitch {
      case off, low, high
      
      mutating func next() {
          switch self {
          case .off:
              self = .low
          case .low:
              self = .high
          case .high:
              self = .off
          }
      }
  }

  var switchState = TriStateSwitch.off
  switchState.next()
  print(switchState) // 출력: low
  ```

---

## **6. Key Points to Remember**

1. **Instance vs Type Methods**:
   - 인스턴스 메서드는 특정 인스턴스에 대해 동작하며, `self`를 통해 인스턴스 속성에 접근할 수 있습니다.
   - 타입 메서드는 타입 자체에서 호출되며, `static` 또는 `class` 키워드로 정의됩니다.

2. **Mutating Methods**:
   - 구조체나 열거형에서 인스턴스 속성을 변경하려면 `mutating` 키워드를 사용해야 합니다.

3. **Self Property**:
   - `self`는 현재 인스턴스를 나타내며, 이름 충돌을 방지하거나 명확성을 위해 사용됩니다.

4. **Enumerations and Structures**:
   - 열거형과 구조체에서도 메서드를 정의할 수 있으며, 이를 통해 상태 변경이나 로직 처리를 구현할 수 있습니다.

