---
title: Collection Type
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---


## **목차**
1. **Mutability of Collections (컬렉션의 가변성)**
2. **Arrays (배열)**
   - 배열 생성 및 초기화
   - 배열 접근 및 수정
3. **Sets (셋)**
   - 셋 생성 및 초기화
   - 셋 연산
4. **Dictionaries (딕셔너리)**
   - 딕셔너리 생성 및 초기화
   - 딕셔너리 접근 및 수정

---

### **1. Mutability of Collections (컬렉션의 가변성)**
- **가변성(Mutability):**
  - 컬렉션(배열, 셋, 딕셔너리)은 `var`로 선언하면 변경 가능(가변적), `let`으로 선언하면 불변.
  - 예:
    ```swift
    var mutableArray = [1, 2, 3] // 변경 가능
    let immutableArray = [1, 2, 3] // 변경 불가능
    ```

- **주의사항:**
  - 컬렉션이 가변적인지 여부는 컬렉션의 타입 자체가 아니라 선언 방식에 따라 결정됨.

---

### **2. Arrays (배열)**

#### **배열 생성 및 초기화**
- **배열 선언:**
  - 형식: `[Element]`
  - 예:
    ```swift
    var someInts: [Int] = [1, 2, 3]
    var emptyArray: [String] = []
    ```

- **빈 배열 초기화:**
  - `[]` 또는 `Array<Element>()` 사용.
  - 예:
    ```swift
    var emptyArray1: [String] = []
    var emptyArray2 = [String]()
    ```

- **기본값으로 초기화:**
  - 특정 값으로 배열을 채우기.
  - 예:
    ```swift
    var threeDoubles = Array(repeating: 0.0, count: 3) // [0.0, 0.0, 0.0]
    ```

#### **배열 접근 및 수정**
- **요소 추가:**
  - `append(_:)` 메서드 또는 `+=` 연산자 사용.
  - 예:
    ```swift
    var shoppingList = ["Eggs", "Milk"]
    shoppingList.append("Flour")
    shoppingList += ["Baking Powder"] // ["Eggs", "Milk", "Flour", "Baking Powder"]
    ```

- **요소 삭제:**
  - `remove(at:)`, `removeLast()` 메서드 사용.
  - 예:
    ```swift
    shoppingList.remove(at: 0) // "Eggs" 제거
    shoppingList.removeLast()  // 마지막 요소 제거
    ```

- **요소 접근:**
  - 인덱스를 사용하여 접근.
  - 예:
    ```swift
    let firstItem = shoppingList[0]
    ```

- **범위로 수정:**
  - 특정 범위의 요소를 새로운 값으로 대체.
  - 예:
    ```swift
    shoppingList[1...3] = ["Bananas", "Apples"]
    ```

---

### **3. Sets (셋)**

#### **셋 생성 및 초기화**
- **셋 선언:**
  - 형식: `Set<Element>`
  - 예:
    ```swift
    var letters: Set<Character> = ["a", "b", "c"]
    ```

- **빈 셋 초기화:**
  - `Set<Element>()` 사용.
  - 예:
    ```swift
    var emptySet: Set<Int> = []
    ```

#### **셋 연산**
- **삽입 및 삭제:**
  - `insert(_:)`, `remove(_:)` 메서드 사용.
  - 예:
    ```swift
    letters.insert("d")
    letters.remove("a")
    ```

- **집합 연산:**
  - 교집합, 합집합, 차집합 등을 계산.
  - 예:
    ```swift
    let oddDigits: Set = [1, 3, 5, 7, 9]
    let evenDigits: Set = [0, 2, 4, 6, 8]
    let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

    oddDigits.union(evenDigits).sorted() // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    oddDigits.intersection(evenDigits).sorted() // []
    ```

- **멤버십 및 동등성 확인:**
  - `contains(_:)`, `==` 연산자 사용.
  - 예:
    ```swift
    if letters.contains("a") {
        print("The set contains 'a'")
    }
    ```

---

### **4. Dictionaries (딕셔너리)**

#### **딕셔너리 생성 및 초기화**
- **딕셔너리 선언:**
  - 형식: `[Key: Value]`
  - 예:
    ```swift
    var namesOfIntegers: [Int: String] = [1: "One", 2: "Two"]
    ```

- **빈 딕셔너리 초기화:**
  - `[:]` 또는 `[Key: Value]()` 사용.
  - 예:
    ```swift
    var emptyDictionary: [String: Int] = [:]
    ```

#### **딕셔너리 접근 및 수정**
- **값 추가 및 업데이트:**
  - 키를 사용하여 값을 추가하거나 업데이트.
  - 예:
    ```swift
    var airports: [String: String] = ["YYZ": "Toronto Pearson"]
    airports["LAX"] = "Los Angeles International"
    airports["YYZ"] = "Toronto Pearson International"
    ```

- **값 삭제:**
  - `removeValue(forKey:)` 메서드 사용.
  - 예:
    ```swift
    airports.removeValue(forKey: "LAX")
    ```

- **값 접근:**
  - 키를 사용하여 접근.
  - 예:
    ```swift
    if let airportName = airports["YYZ"] {
        print("The name of the airport is \(airportName)")
    }
    ```

- **전체 순회:**
  - `for-in` 루프를 사용하여 키와 값 순회.
  - 예:
    ```swift
    for (airportCode, airportName) in airports {
        print("\(airportCode): \(airportName)")
    }
    ```

