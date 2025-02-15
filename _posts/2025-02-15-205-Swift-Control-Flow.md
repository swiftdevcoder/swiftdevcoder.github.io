---
title: 05.Control Flow
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---


## **목차**
1. **For-In Loops (for-in 루프)**
2. **While Loops (while 루프)**
   - `while`
   - `repeat-while`
3. **Conditional Statements (조건문)**
   - `if`
   - `else if`
   - `switch`
4. **Control Transfer Statements (제어 전환 문)**
   - `continue`
   - `break`
   - `fallthrough`
   - `return`
5. **Labeled Statements (레이블 문)**
6. **Early Exit (조기 종료)**
   - `guard`
7. **Checking API Availability (API 가용성 확인)**

---

### **1. For-In Loops (for-in 루프)**
- **배열, 범위, 문자열 등 반복 가능한 항목들을 순회.**
- 형식:
  ```swift
  for item in items {
      // 작업 수행
  }
  ```

- **예제:**
  ```swift
  let names = ["Anna", "Alex", "Brian", "Jack"]
  for name in names {
      print("Hello, \(name)!")
  }
  ```

- **범위 순회:**
  ```swift
  for index in 1...5 {
      print("\(index) times 5 is \(index * 5)")
  }
  ```

- **튜플 분해:**
  ```swift
  let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
  for (animalName, legCount) in numberOfLegs {
      print("\(animalName)s have \(legCount) legs")
  }
  ```

---

### **2. While Loops (while 루프)**

#### **`while`**
- 조건이 `true`인 동안 반복.
- 형식:
  ```swift
  while condition {
      // 작업 수행
  }
  ```

- **예제:**
  ```swift
  var i = 0
  while i < 5 {
      print(i)
      i += 1
  }
  ```

#### **`repeat-while`**
- 최소 한 번은 실행한 후 조건을 확인.
- 형식:
  ```swift
  repeat {
      // 작업 수행
  } while condition
  ```

- **예제:**
  ```swift
  var j = 0
  repeat {
      print(j)
      j += 1
  } while j < 5
  ```

---

### **3. Conditional Statements (조건문)**

#### **`if`**
- 조건에 따라 코드 블록 실행.
- 형식:
  ```swift
  if condition {
      // 작업 수행
  }
  ```

- **예제:**
  ```swift
  let temperature = 25
  if temperature > 30 {
      print("It's really warm.")
  }
  ```

#### **`else if`**
- 여러 조건을 검사.
- 형식:
  ```swift
  if condition1 {
      // 작업 수행
  } else if condition2 {
      // 작업 수행
  } else {
      // 기본 작업 수행
  }
  ```

- **예제:**
  ```swift
  let score = 85
  if score >= 90 {
      print("Grade A")
  } else if score >= 80 {
      print("Grade B")
  } else {
      print("Grade C")
  }
  ```

#### **`switch`**
- 값에 따라 여러 경우를 처리.
- 형식:
  ```swift
  switch value {
  case pattern1:
      // 작업 수행
  case pattern2:
      // 작업 수행
  default:
      // 기본 작업 수행
  }
  ```

- **예제:**
  ```swift
  let vegetable = "red pepper"
  switch vegetable {
  case "celery":
      print("Add some raisins and make ants on a log.")
  case "cucumber", "watercress":
      print("That would make a good tea sandwich.")
  case let x where x.hasSuffix("pepper"):
      print("Is it a spicy \(x)?")
  default:
      print("Everything tastes good in soup.")
  }
  ```

- **특징:**
  - `default`가 반드시 필요하지 않음(모든 경우를 처리하면 생략 가능).
  - `where`를 사용하여 추가 조건 지정 가능.

---

### **4. Control Transfer Statements (제어 전환 문)**

#### **`continue`**
- 현재 반복을 건너뛰고 다음 반복으로 넘어감.
- 예:
  ```swift
  for number in 1...10 {
      if number % 2 == 0 {
          continue
      }
      print(number)
  }
  ```

#### **`break`**
- 반복문 또는 `switch` 문을 즉시 종료.
- 예:
  ```swift
  for number in 1...10 {
      if number == 5 {
          break
      }
      print(number)
  }
  ```

#### **`fallthrough`**
- `switch` 문에서 다음 케이스로 넘어감.
- 예:
  ```swift
  let integerToDescribe = 5
  var description = "The number \(integerToDescribe) is"
  switch integerToDescribe {
  case 2, 3, 5, 7, 11, 13:
      description += " a prime number, and also"
      fallthrough
  default:
      description += " an integer."
  }
  print(description)
  ```

#### **`return`**
- 함수에서 값을 반환하거나 종료.
- 예:
  ```swift
  func greet(name: String) -> String {
      return "Hello, \(name)!"
  }
  ```

---

### **5. Labeled Statements (레이블 문)**
- 중첩된 루프나 조건문에서 특정 블록을 식별.
- 형식:
  ```swift
  labelName: for item in items {
      // 작업 수행
  }
  ```

- **예제:**
  ```swift
  outerLoop: for i in 1...5 {
      for j in 1...5 {
          if j == 3 {
              break outerLoop
          }
          print("i: \(i), j: \(j)")
      }
  }
  ```

---

### **6. Early Exit (조기 종료)**
- `guard`를 사용하여 조건이 충족되지 않을 때 조기에 종료.
- 형식:
  ```swift
  guard condition else {
      // 조기 종료 작업
      return
  }
  ```

- **예제:**
  ```swift
  func greet(person: [String: String]) {
      guard let name = person["name"] else {
          print("Name is missing")
          return
      }
      print("Hello, \(name)!")
  }
  ```

---

### **7. Checking API Availability (API 가용성 확인)**
- 특정 플랫폼 또는 버전에서 API를 사용할 수 있는지 확인.
- 형식:
  ```swift
  if #available(iOS 15, macOS 12, *) {
      // iOS 15 이상 또는 macOS 12 이상에서 실행
  } else {
      // 이전 버전에서 실행
  }
  ```

- **예제:**
  ```swift
  if #available(iOS 14, *) {
      print("This feature is available on iOS 14 and later.")
  } else {
      print("This feature is not available on your version of iOS.")
  }
  ```
