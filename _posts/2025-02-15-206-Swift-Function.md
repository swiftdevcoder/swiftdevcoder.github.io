---
title: Function
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Functions (함수)**
2. **Parameters and Return Values (매개변수와 반환값)**
3. **External Parameter Names (외부 매개변수 이름)**
4. **Default Parameter Values (기본 매개변수 값)**
5. **Variadic Parameters (가변 매개변수)**
6. **In-Out Parameters (In-Out 매개변수)**
7. **Function Types (함수 타입)**
8. **Nested Functions (중첩 함수)**
9. **Closures and Functions (클로저와 함수의 차이)**

## **Swift Functions (함수)**

### **1. 함수의 기본 구조**
Swift에서 함수는 특정 작업을 수행하는 코드 블록입니다. 함수는 입력(매개변수)을 받아 처리하고, 결과를 반환할 수 있습니다.

#### **기본 문법**
```swift
func functionName(parameterName: ParameterType) -> ReturnType {
    // 함수 본문
    return value
}
```

- `func`: 함수를 정의하기 위한 키워드.
- `functionName`: 함수의 이름.
- `parameterName: ParameterType`: 매개변수 이름과 타입.
- `ReturnType`: 반환값의 타입 (없으면 `Void` 또는 생략 가능).
- `return`: 반환값을 지정.

#### **예시**
```swift
func greet(person: String) -> String {
    return "Hello, \(person)!"
}

let greeting = greet(person: "Alice")
print(greeting) // 출력: Hello, Alice!
```

---

### **2. 매개변수와 반환값**
#### **매개변수가 없는 함수**
매개변수가 없는 함수도 정의할 수 있습니다.
```swift
func sayHello() -> String {
    return "Hello, world!"
}

print(sayHello()) // 출력: Hello, world!
```

#### **반환값이 없는 함수**
반환값이 없는 함수는 `Void`를 반환하거나 반환 타입을 생략합니다.
```swift
func sayGoodbye() {
    print("Goodbye!")
}

sayGoodbye() // 출력: Goodbye!
```

#### **여러 매개변수와 반환값**
여러 매개변수를 받고, 여러 값을 반환할 수도 있습니다.
```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

let result = add(5, 3)
print(result) // 출력: 8
```

---

### **3. 외부 매개변수 이름 (External Parameter Names)**
Swift에서는 함수 호출 시 매개변수 이름을 명확하게 표시할 수 있도록 외부 매개변수 이름을 사용할 수 있습니다.

#### **예시**
```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)."
}

let message = greet(person: "Alice", from: "Seoul")
print(message) // 출력: Hello Alice! Glad you could visit from Seoul.
```

- `from`은 외부 매개변수 이름으로, 함수 호출 시 사용됩니다.

---

### **4. 기본 매개변수 값 (Default Parameter Values)**
매개변수에 기본값을 설정할 수 있습니다. 기본값이 있는 매개변수는 호출 시 생략 가능합니다.

#### **예시**
```swift
func multiply(_ a: Int, by b: Int = 2) -> Int {
    return a * b
}

let result1 = multiply(5) // b의 기본값인 2가 사용됨
print(result1) // 출력: 10

let result2 = multiply(5, by: 3) // b를 명시적으로 3으로 설정
print(result2) // 출력: 15
```

---

### **5. 가변 매개변수 (Variadic Parameters)**
함수는 동일한 타입의 값을 여러 개 받을 수 있습니다. 이를 가변 매개변수라고 합니다.

#### **예시**
```swift
func sum(_ numbers: Int...) -> Int {
    var total = 0
    for number in numbers {
        total += number
    }
    return total
}

let result = sum(1, 2, 3, 4, 5)
print(result) // 출력: 15
```

---

### **6. In-Out 매개변수**
함수 내부에서 매개변수의 값을 변경하고, 그 변경된 값을 함수 외부에서도 반영할 수 있습니다. 이를 위해 `inout` 키워드를 사용합니다.

#### **예시**
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var x = 10
var y = 20
swapTwoInts(&x, &y)
print("x is now \(x), y is now \(y)") // 출력: x is now 20, y is now 10
```

- `&` 기호를 사용하여 변수를 전달해야 합니다.

---

### **7. 함수 타입 (Function Types)**
함수 자체도 타입으로 취급될 수 있습니다. 함수 타입은 매개변수 타입과 반환 타입으로 구성됩니다.

#### **예시**
```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func subtract(_ a: Int, _ b: Int) -> Int {
    return a - b
}

// 함수 타입 선언
var mathFunction: (Int, Int) -> Int = add

print(mathFunction(5, 3)) // 출력: 8

mathFunction = subtract
print(mathFunction(5, 3)) // 출력: 2
```

---

### **8. 중첩 함수 (Nested Functions)**
함수 내부에 다른 함수를 정의할 수 있습니다. 중첩 함수는 외부 함수 내에서만 사용 가능합니다.

#### **예시**
```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    
    return backward ? stepBackward : stepForward
}

let moveNearerToZero = chooseStepFunction(backward: true)
print(moveNearerToZero(5)) // 출력: 4
```

---

### **9. 클로저와 함수의 차이**
함수는 명명된 코드 블록이고, 클로저는 익명의 코드 블록입니다. 클로저는 함수와 유사하지만 더 간결하게 작성할 수 있습니다.

#### **클로저 예시**
```swift
let multiply = { (a: Int, b: Int) -> Int in
    return a * b
}

print(multiply(3, 4)) // 출력: 12
```

---

### **요약**
Swift의 함수는 강력하고 유연한 도구입니다. 다음은 핵심 요점입니다:
1. 매개변수와 반환값을 자유롭게 정의할 수 있음.
2. 외부 매개변수 이름, 기본값, 가변 매개변수 등을 지원.
3. `inout` 매개변수로 값을 수정 가능.
4. 함수 자체도 타입으로 사용 가능.
5. 중첩 함수와 클로저를 활용해 코드를 간결하게 작성 가능.

