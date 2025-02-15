---
title: Subscripts
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Subscripts란?**
2. **Subscripts의 기본 문법**
3. **Subscripts의 매개변수**
4. **Subscripts의 활용 예시**
5. **Subscripts의 특징**
6. **주의사항**

## **Subscripts (하위 스크립트)**

### **1. Subscripts란?**
- Subscripts는 인스턴스의 특정 값을 간편하게 설정하거나 조회할 수 있는 단축 문법을 제공합니다.
- 예를 들어, 배열이나 딕셔너리를 사용할 때 `array[index]` 또는 `dictionary[key]`와 같은 방식으로 데이터에 접근하는 것이 가능합니다.
- 사용자 정의 타입(클래스, 구조체, 열거형)에서도 Subscripts를 정의하여 비슷한 방식으로 데이터를 조작할 수 있습니다.

### **2. Subscripts의 기본 문법**
Subscripts는 `subscript` 키워드를 사용하여 정의됩니다. 기본적인 형식은 다음과 같습니다:

```swift
subscript(index: Int) -> Int {
    get {
        // subscript를 통해 값을 반환하는 코드
    }
    set(newValue) {
        // subscript를 통해 값을 설정하는 코드
    }
}
```

- **읽기 전용 Subscripts**: 만약 Subscripts가 읽기만 가능하다면 `get`과 `set`을 생략하고 바로 값을 반환하도록 구현할 수 있습니다.

```swift
subscript(index: Int) -> Int {
    return someArray[index]
}
```

### **3. Subscripts의 매개변수**
- Subscripts는 하나 이상의 매개변수를 가질 수 있으며, 매개변수의 타입은 제한이 없습니다.
- 매개변수 이름은 외부 이름과 내부 이름을 모두 가질 수 있습니다. 외부 이름은 호출 시 사용되고, 내부 이름은 구현 내부에서 사용됩니다.

예시:
```swift
struct Matrix {
    var grid: [[Int]]

    subscript(row: Int, column: Int) -> Int {
        get {
            return grid[row][column]
        }
        set {
            grid[row][column] = newValue
        }
    }
}
```

위의 예시에서는 행(`row`)과 열(`column`) 두 개의 매개변수를 사용하여 2차원 배열의 값을 접근하거나 수정할 수 있습니다.

### **4. Subscripts의 활용 예시**
#### (1) 읽기/쓰기 가능한 Subscripts
```swift
struct TimesTable {
    let multiplier: Int

    subscript(index: Int) -> Int {
        return multiplier * index
    }
}

let threeTimesTable = TimesTable(multiplier: 3)
print(threeTimesTable[6]) // 출력: 18
```

#### (2) 읽기 전용 Subscripts
```swift
struct FibonacciSequence {
    private var sequence: [Int] = [0, 1]

    subscript(index: Int) -> Int {
        while sequence.count <= index {
            let nextValue = sequence[sequence.count - 1] + sequence[sequence.count - 2]
            sequence.append(nextValue)
        }
        return sequence[index]
    }
}

let fib = FibonacciSequence()
print(fib[7]) // 출력: 13
```

### **5. Subscripts의 특징**
- **다양한 매개변수 타입 지원**: Subscripts는 정수뿐만 아니라 문자열, 부동소수점 등 다양한 타입의 매개변수를 사용할 수 있습니다.
- **오버로딩 가능**: 동일한 타입 내에서 여러 개의 Subscripts를 정의할 수 있습니다. 이때 매개변수의 개수나 타입에 따라 적절한 Subscripts가 선택됩니다.
- **타입 프로퍼티에도 적용 가능**: `static` 키워드를 사용하여 타입 자체에 Subscripts를 정의할 수도 있습니다.

```swift
struct LevelTracker {
    static var highestUnlockedLevel = 1

    static subscript(level: Int) -> Bool {
        get {
            return level <= highestUnlockedLevel
        }
        set {
            if newValue && level > highestUnlockedLevel {
                highestUnlockedLevel = level
            }
        }
    }
}

LevelTracker[3] = true
print(LevelTracker.highestUnlockedLevel) // 출력: 3
```

### **6. 주의사항**
- Subscripts는 단순히 데이터를 접근하거나 설정하기 위한 단축 문법일 뿐, 복잡한 로직을 포함시키는 것은 피해야 합니다.
- Subscripts의 목적은 직관적이고 간결한 인터페이스를 제공하는 것이므로, 과도하게 많은 매개변수를 사용하거나 복잡한 연산을 수행하는 것은 권장되지 않습니다.

