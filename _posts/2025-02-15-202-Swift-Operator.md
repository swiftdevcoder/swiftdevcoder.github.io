---
title: 02.Swift Operator
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---


## **목차**
1. **Terminology (용어 설명)**
2. **Assignment Operator (할당 연산자)**
3. **Arithmetic Operators (산술 연산자)**
4. **Compound Assignment Operators (복합 할당 연산자)**
5. **Comparison Operators (비교 연산자)**
6. **Ternary Conditional Operator (삼항 조건 연산자)**
7. **Nil-Coalescing Operator (Nil 병합 연산자)**
8. **Range Operators (범위 연산자)**
9. **Logical Operators (논리 연산자)**

---

### **1. Terminology (용어 설명)**
- **Operand (피연산자):**
  - 연산자가 작동하는 값.
  - 예: `1 + 2`에서 `1`과 `2`가 피연산자.

- **Unary Operator (단항 연산자):**
  - 하나의 피연산자에만 작동.
  - 예: `-a` (음수 변환), `!b` (논리 NOT).

- **Binary Operator (이항 연산자):**
  - 두 개의 피연산자에 작동.
  - 예: `a + b`, `c * d`.

- **Ternary Operator (삼항 연산자):**
  - 세 개의 피연산자에 작동.
  - Swift에서는 삼항 조건 연산자(`? :`)만 존재.

---

### **2. Assignment Operator (할당 연산자)**
- 변수에 값을 할당하는 연산자 (`=`).
- 예:
  ```swift
  let b = 10
  var a = 5
  a = b // a의 값은 이제 10
  ```

- **주의사항:**
  - Swift의 할당 연산자는 다른 언어와 달리 표현식으로 평가되지 않음.
  - 예: `if x = y`와 같은 코드는 에러 발생.

---

### **3. Arithmetic Operators (산술 연산자)**
- 기본적인 수학 연산을 수행.
- **주요 연산자:**
  - `+`: 덧셈
  - `-`: 뺄셈
  - `*`: 곱셈
  - `/`: 나눗셈
  - `%`: 나머지(모듈러)

- 예:
  ```swift
  let sum = 1 + 2       // 3
  let difference = 5 - 3 // 2
  let product = 2 * 3    // 6
  let quotient = 10 / 3  // 3
  let remainder = 10 % 3 // 1
  ```

- **부동소수점 연산:**
  - 부동소수점 숫자에서도 동일하게 작동.
  - 예: `8.0 / 2.5` → `3.2`

---

### **4. Compound Assignment Operators (복합 할당 연산자)**
- 산술 연산과 할당 연산을 결합.
- **형식:** `변수 연산자= 값`
- 예:
  ```swift
  var a = 1
  a += 2 // a = a + 2 → 결과: 3
  a -= 1 // a = a - 1 → 결과: 2
  a *= 3 // a = a * 3 → 결과: 6
  a /= 2 // a = a / 2 → 결과: 3
  ```

---

### **5. Comparison Operators (비교 연산자)**
- 두 값을 비교하여 `true` 또는 `false`를 반환.
- **주요 연산자:**
  - `==`: 같음
  - `!=`: 같지 않음
  - `>`: 초과
  - `<`: 미만
  - `>=`: 이상
  - `<=`: 이하

- 예:
  ```swift
  let isEqual = (1 == 1)      // true
  let isNotEqual = (1 != 2)   // true
  let isGreater = (5 > 3)     // true
  ```

- **튜플 비교:**
  - 튜플도 비교 가능하며, 왼쪽부터 순서대로 비교.
  - 예:
    ```swift
    (1, "zebra") < (2, "apple") // true (첫 번째 요소 비교)
    (3, "apple") < (3, "bird")  // true (두 번째 요소 비교)
    ```

---

### **6. Ternary Conditional Operator (삼항 조건 연산자)**
- 조건에 따라 두 가지 값 중 하나를 선택.
- **형식:** `조건 ? 값1 : 값2`
- 예:
  ```swift
  let contentHeight = 40
  let hasHeader = true
  let rowHeight = contentHeight + (hasHeader ? 50 : 20)
  // hasHeader가 true이므로 rowHeight는 90
  ```

---

### **7. Nil-Coalescing Operator (Nil 병합 연산자)**
- 옵셔널 값이 `nil`인지 확인하고, `nil`일 경우 기본값을 제공.
- **형식:** `옵셔널 ?? 기본값`
- 예:
  ```swift
  let defaultColorName = "red"
  var userDefinedColorName: String? = nil
  let colorNameToUse = userDefinedColorName ?? defaultColorName
  // userDefinedColorName이 nil이므로 colorNameToUse는 "red"
  ```

---

### **8. Range Operators (범위 연산자)**
- 일정 범위의 값을 표현.
- **주요 연산자:**
  - **Closed Range (`...`):** 시작값과 끝값 모두 포함.
    - 예: `1...5` → 1, 2, 3, 4, 5
  - **Half-Open Range (`..<`):** 시작값 포함, 끝값 미포함.
    - 예: `1..<5` → 1, 2, 3, 4

- **One-Sided Ranges (한쪽 방향 범위):**
  - 시작값이나 끝값 중 하나만 지정.
  - 예:
    ```swift
    let names = ["Anna", "Alex", "Brian", "Jack"]
    let firstTwo = names[..<2] // ["Anna", "Alex"]
    let lastTwo = names[2...]  // ["Brian", "Jack"]
    ```

---

### **9. Logical Operators (논리 연산자)**
- 논리적 조건을 평가.
- **주요 연산자:**
  - `!`: NOT (부정)
  - `&&`: AND (논리곱)
  - `||`: OR (논리합)

- **예제:**
  ```swift
  let allowEntry = false
  if !allowEntry {
      print("ACCESS DENIED")
  }

  let enteredDoorCode = true
  let passedRetinaScan = false
  if enteredDoorCode && passedRetinaScan {
      print("Welcome!")
  } else {
      print("ACCESS DENIED")
  }
  ```

- **Short-Circuit Evaluation (단락 평가):**
  - `&&`는 첫 번째 값이 `false`면 두 번째 값을 평가하지 않음.
  - `||`는 첫 번째 값이 `true`면 두 번째 값을 평가하지 않음.

