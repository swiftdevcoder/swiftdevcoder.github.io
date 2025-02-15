---
title: 10.Properties
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Stored Properties (저장 속성)**  
2. **Computed Properties (계산 속성)**  
3. **Property Observers (속성 감시자)**  
4. **Type Properties (타입 속성)**  
5. **Property Wrappers (속성 래퍼)**

## **속성(Properties)이란?**
Swift에서 속성은 특정 타입(클래스, 구조체, 열거형)과 연관된 값을 나타냅니다. 속성은 두 가지 주요 카테고리로 나뉩니다:
1. **Stored Properties (저장 속성)**  
   - 상수(`let`) 또는 변수(`var`) 형태로 값을 저장합니다.
   - 주로 클래스와 구조체에서 사용됩니다.

2. **Computed Properties (계산 속성)**  
   - 값 자체를 저장하지 않고, 다른 속성이나 값을 기반으로 계산된 결과를 제공합니다.
   - 클래스, 구조체, 열거형에서 모두 사용 가능합니다.

---

### **1. Stored Properties (저장 속성)**

저장 속성은 인스턴스가 생성될 때 메모리에 값을 저장하는 속성입니다.  
- `var`: 가변적인 값을 저장할 수 있음.
- `let`: 불변적인 값을 저장함.

#### 예시:
```swift
struct FixedLengthRange {
    var firstValue: Int // 가변적
    let length: Int     // 불변적
}

var range = FixedLengthRange(firstValue: 0, length: 3)
range.firstValue = 5 // 변경 가능
// range.length = 4  // 에러: length는 불변적임
```

#### Lazy Stored Properties
- 초기화가 지연되는 속성으로, 처음 접근되기 전까지는 초기화되지 않습니다.
- 키워드 `lazy`를 사용하여 선언합니다.

#### 예시:
```swift
class DataImporter {
    var fileName = "data.txt"
}

class DataManager {
    lazy var importer = DataImporter() // 필요할 때 초기화됨
    var data: [String] = []
}

let manager = DataManager()
manager.data.append("Some data")
// importer는 아직 초기화되지 않음
print(manager.importer.fileName) // 여기서야 importer가 초기화됨
```

---

### **2. Computed Properties (계산 속성)**

계산 속성은 값을 저장하지 않고, 다른 속성을 기반으로 값을 계산하거나 설정합니다.  
- `get`: 값을 반환하는 코드 블록.
- `set`: 값을 설정하는 코드 블록 (옵션).

#### 예시:
```swift
struct Point {
    var x = 0.0, y = 0.0
}

struct Size {
    var width = 0.0, height = 0.0
}

struct Rect {
    var origin = Point()
    var size = Size()
    
    // 계산 속성: 넓이를 계산
    var area: Double {
        return size.width * size.height
    }
    
    // 읽기/쓰기 가능한 계산 속성
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}

var square = Rect(origin: Point(x: 0.0, y: 0.0), size: Size(width: 10.0, height: 10.0))
print(square.area) // 출력: 100.0
square.center = Point(x: 15.0, y: 15.0)
print(square.origin) // 출력: x: 10.0, y: 10.0
```

---

### **3. Property Observers**

속성의 값이 변경될 때 추가 작업을 수행할 수 있는 기능입니다.  
- `willSet`: 값이 변경되기 직전에 호출.
- `didSet`: 값이 변경된 직후에 호출.

#### 예시:
```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}

let counter = StepCounter()
counter.totalSteps = 200
// 출력:
// About to set totalSteps to 200
// Added 200 steps
```

---

### **4. Type Properties**

인스턴스가 아닌 타입 자체에 속하는 속성입니다.  
- `static`: 구조체와 열거형에서 사용.
- `class`: 클래스에서 사용 (상속 가능).

#### 예시:
```swift
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 42
    }
}

class SomeClass {
    static var storedTypeProperty = "Some value."
    class var computedTypeProperty: Int {
        return 42
    }
}

print(SomeStructure.storedTypeProperty) // 출력: Some value.
print(SomeClass.computedTypeProperty)   // 출력: 42
```

---

### **5. Property Wrappers**

속성의 동작을 캡슐화하는 방법으로, 재사용 가능한 속성 동작을 정의할 수 있습니다.  
`@propertyWrapper` 어노테이션을 사용하여 정의합니다.

#### 예시:
```swift
@propertyWrapper
struct TwelveOrLess {
    private var number = 0
    var wrappedValue: Int {
        get { return number }
        set { number = min(newValue, 12) }
    }
}

struct SmallRectangle {
    @TwelveOrLess var height: Int
    @TwelveOrLess var width: Int
}

var rectangle = SmallRectangle()
rectangle.height = 15
print(rectangle.height) // 출력: 12
```

---

### **정리**
Swift의 속성(Properties)은 데이터를 저장하거나 계산하는 다양한 방식을 제공하며, 이를 통해 유연하고 강력한 코드를 작성할 수 있습니다. 핵심 개념은 다음과 같습니다:
1. **Stored Properties**: 값을 직접 저장.
2. **Computed Properties**: 값을 계산하여 제공.
3. **Property Observers**: 값 변경 시 추가 작업 수행.
4. **Type Properties**: 타입 자체에 속하는 속성.
5. **Property Wrappers**: 속성 동작을 캡슐화.
