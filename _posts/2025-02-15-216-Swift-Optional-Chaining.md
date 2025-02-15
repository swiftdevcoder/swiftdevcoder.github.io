---
title: Optional Chaining
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **옵셔널 체이닝(Optional Chaining)이란?**
2. **옵셔널 체이닝의 기본 문법**
3. **옵셔널 체이닝의 주요 사용 사례**
4. **옵셔널 체이닝과 강제 언래핑의 차이**
5. **옵셔널 체이닝의 결과 타입**
6. **옵셔널 체이닝의 장점**


## **옵셔널 체이닝(Optional Chaining)이란?**
옵셔널 체이닝은 옵셔널 값에 접근하거나 메서드를 호출할 때, 해당 옵셔널이 `nil`인지 아닌지를 확인하면서 안전하게 작업을 수행할 수 있는 방법입니다. 만약 옵셔널 값이 `nil`이라면, 옵셔널 체이닝은 실패하지만 앱이 크래시되지 않습니다. 대신 결과값으로 `nil`을 반환합니다.

옵셔널 체이닝은 특히 복잡한 객체 계층 구조에서 유용합니다. 예를 들어, 여러 단계의 프로퍼티나 메서드를 연속적으로 호출해야 하는 경우, 각 단계마다 `nil`을 확인하지 않고도 안전하게 작업을 수행할 수 있습니다.

---

### **옵셔널 체이닝의 기본 문법**
옵셔널 체이닝은 물음표(`?`)를 사용하여 표현합니다. 이는 "이 값이 `nil`이 아니라면 다음 작업을 수행하라"는 의미입니다.

```swift
let result = someOptional?.someProperty
```

- `someOptional`이 `nil`이 아니면 `someProperty`에 접근합니다.
- `someOptional`이 `nil`이면 전체 표현식의 결과는 `nil`이 됩니다.

---

### **옵셔널 체이닝의 주요 사용 사례**

#### 1. **프로퍼티 접근**
옵셔널 체이닝을 사용하여 옵셔널 타입의 인스턴스가 가지고 있는 프로퍼티에 접근할 수 있습니다.

```swift
class Person {
    var residence: Residence?
}

class Residence {
    var numberOfRooms = 1
}

let john = Person()

// 옵셔널 체이닝을 사용한 프로퍼티 접근
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
```

위 예제에서 `john.residence`가 `nil`이므로, `numberOfRooms`에 접근하지 못하고 `else` 블록이 실행됩니다.

---

#### 2. **메서드 호출**
옵셔널 체이닝을 사용하여 옵셔널 값의 메서드를 호출할 수도 있습니다. 메서드가 성공적으로 호출되었는지 여부를 확인할 수 있습니다.

```swift
func printNumberOfRooms() {
    print("Number of rooms printed.")
}

let john = Person()
john.residence?.printNumberOfRooms() // residence가 nil이므로 메서드 호출이 실행되지 않음
```

---

#### 3. **서브스크립트(Subscript) 접근**
옵셔널 체이닝을 사용하여 서브스크립트에도 접근할 수 있습니다.

```swift
class Residence {
    var rooms = ["Living Room", "Bedroom"]
    subscript(index: Int) -> String? {
        return rooms.indices.contains(index) ? rooms[index] : nil
    }
}

let john = Person()
if let firstRoom = john.residence?[0] {
    print("The first room is \(firstRoom).")
} else {
    print("Unable to access the room.")
}
```

---

#### 4. **다중 옵셔널 체이닝**
여러 단계의 옵셔널 체이닝을 연결할 수 있습니다. 이는 깊이 중첩된 객체 구조에서 유용합니다.

```swift
class Address {
    var buildingName: String?
}

class Residence {
    var address: Address?
}

class Person {
    var residence: Residence?
}

let john = Person()
if let buildingName = john.residence?.address?.buildingName {
    print("John's building name is \(buildingName).")
} else {
    print("Unable to retrieve the building name.")
}
```

---

### **옵셔널 체이닝과 강제 언래핑의 차이**
옵셔널 체이닝은 안전하게 값을 접근하거나 메서드를 호출하는 반면, 강제 언래핑(`!`)은 옵셔널 값이 반드시 존재한다고 가정합니다. 만약 강제 언래핑 시도 시 값이 `nil`이라면 런타임 에러가 발생합니다.

```swift
let roomCount = john.residence!.numberOfRooms // residence가 nil이면 크래시 발생
```

따라서, 가능하다면 강제 언래핑보다는 옵셔널 체이닝을 사용하는 것이 안전합니다.

---

### **옵셔널 체이닝의 결과 타입**
옵셔널 체이닝의 결과는 항상 옵셔널 타입입니다. 따라서 결과값을 사용하기 전에 반드시 옵셔널 바인딩이나 다른 방식으로 언래핑해야 합니다.

```swift
let roomCount: Int? = john.residence?.numberOfRooms
```

---

### **옵셔널 체이닝의 장점**
1. **안전성**: `nil` 값으로 인한 런타임 에러를 방지합니다.
2. **간결성**: 복잡한 조건문 없이도 간단히 옵셔널 값을 처리할 수 있습니다.
3. **유연성**: 여러 단계의 객체 계층 구조에서도 쉽게 접근할 수 있습니다.

---

### **요약**
옵셔널 체이닝은 Swift에서 옵셔널 값에 접근하거나 메서드를 호출할 때 매우 유용한 기능입니다. 이를 통해 `nil` 값을 안전하게 처리할 수 있으며, 코드를 더 간결하고 읽기 쉽게 만들 수 있습니다. 옵셔널 체이닝은 다음과 같은 상황에서 사용됩니다:
- 프로퍼티 접근
- 메서드 호출
- 서브스크립트 접근
- 다중 체이닝

