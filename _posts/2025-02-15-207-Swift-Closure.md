---
title: Closure
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **클로저란?**
2. **클로저의 기본 구조**
3. **클로저의 종류**
4. **클로저의 문법 축약**
5. **클로저의 캡처링(Capturing Values)**
6. **클로저의 활용 예시**
7. **클로저의 주의사항**



## **1. 클로저란?**
클로저는 독립적으로 실행 가능한 코드 블록으로, 변수나 상수에 저장하거나 함수의 매개변수로 전달할 수 있습니다. 클로저는 다음과 같은 특징을 가집니다:
- **자체적인 문맥을 캡처**: 클로저는 자신이 정의된 주변 문맥(context)의 값을 참조할 수 있습니다.
- **간결한 문법**: 필요에 따라 문법을 축약하여 표현할 수 있습니다.
- **함수와 유사**: 클로저는 익명 함수(anonymous function)로도 볼 수 있습니다.

---

## **2. 클로저의 기본 구조**
Swift에서 클로저의 일반적인 형식은 다음과 같습니다:

```swift
{ (parameters) -> ReturnType in
    statements
}
```

- **parameters**: 클로저가 받는 입력 매개변수 목록입니다.
- **ReturnType**: 클로저가 반환하는 값의 타입입니다.
- **in**: 매개변수와 반환 타입을 구분하며, 이후에 실행될 코드를 나타냅니다.

예시:
```swift
let sayHello: (String) -> String = { (name: String) -> String in
    return "Hello, \(name)!"
}

print(sayHello("Alice")) // 출력: Hello, Alice!
```

---

## **3. 클로저의 종류**
Swift에서는 세 가지 유형의 클로저를 제공합니다:

### 1) **전역 함수(Global Function)**
매개변수가 있고 반환값이 있는 일반적인 함수입니다. 클로저와 달리 이름이 있으며 외부 문맥을 캡처하지 않습니다.

```swift
func addTwoNumbers(a: Int, b: Int) -> Int {
    return a + b
}
```

### 2) **중첩 함수(Nested Function)**
다른 함수 내부에 정의된 함수입니다. 외부 함수의 변수를 캡처할 수 있습니다.

```swift
func makeIncrementer() -> (Int) -> Int {
    var runningTotal = 0
    func incrementer(amount: Int) -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

let incrementByTen = makeIncrementer()
print(incrementByTen(10)) // 출력: 10
print(incrementByTen(5))  // 출력: 15
```

### 3) **클로저 표현식(Closure Expression)**
가장 일반적인 클로저 형태로, 간결하게 작성할 수 있습니다.

```swift
let multiply = { (a: Int, b: Int) -> Int in
    return a * b
}

print(multiply(3, 4)) // 출력: 12
```

---

## **4. 클로저의 문법 축약**
Swift는 클로저를 더욱 간결하게 작성할 수 있도록 다양한 문법적 편의를 제공합니다.

### 1) **타입 추론(Type Inference)**
매개변수와 반환 타입을 명시적으로 작성하지 않아도 컴파일러가 자동으로 추론합니다.

```swift
let divide = { (a: Int, b: Int) in
    return a / b
}

print(divide(10, 2)) // 출력: 5
```

### 2) **단축 인자 이름(Shorthand Argument Names)**
매개변수 이름 대신 `$0`, `$1` 등의 단축 인자 이름을 사용할 수 있습니다.

```swift
let sum = { $0 + $1 }
print(sum(3, 5)) // 출력: 8
```

### 3) **암시적 반환(Implicit Returns)**
클로저의 본문이 한 줄로 구성되어 있다면 `return` 키워드를 생략할 수 있습니다.

```swift
let greet = { "Hello, \($0)!" }
print(greet("Bob")) // 출력: Hello, Bob!
```

---

## **5. 클로저의 캡처링(Capturing Values)**
클로저는 자신이 정의된 문맥의 값을 캡처하여 사용할 수 있습니다. 이를 통해 클로저는 외부 변수를 참조하거나 수정할 수 있습니다.

```swift
func makeCounter() -> () -> Int {
    var count = 0
    let increment: () -> Int = {
        count += 1
        return count
    }
    return increment
}

let counter = makeCounter()
print(counter()) // 출력: 1
print(counter()) // 출력: 2
```

---

## **6. 클로저의 활용 예시**
클로저는 다양한 상황에서 유용하게 사용됩니다. 대표적인 예시는 다음과 같습니다:

### 1) **정렬(Sorting)**
배열을 정렬할 때 클로저를 사용할 수 있습니다.

```swift
let numbers = [5, 2, 8, 1]
let sortedNumbers = numbers.sorted { $0 < $1 }
print(sortedNumbers) // 출력: [1, 2, 5, 8]
```

### 2) **비동기 작업(Asynchronous Operations)**
네트워크 요청이나 타이머와 같은 비동기 작업에서 클로저를 활용할 수 있습니다.

```swift
DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
    print("This will be printed after 2 seconds.")
}
```

---

## **7. 클로저의 주의사항**
- **순환 참조(Circular Reference)**: 클로저가 자신을 포함하는 객체를 강하게 참조하면 메모리 누수가 발생할 수 있습니다. 이를 방지하기 위해 `[weak self]` 또는 `[unowned self]`를 사용합니다.
  
```swift
class ViewController {
    var closure: (() -> Void)?
    
    func setupClosure() {
        closure = { [weak self] in
            self?.doSomething()
        }
    }
    
    func doSomething() {
        print("Doing something...")
    }
}
```

---

## **요약**
- 클로저는 독립적으로 실행 가능한 코드 블록으로, 함수보다 더 유연하고 간결하게 사용할 수 있습니다.
- 클로저는 매개변수, 반환 타입, 본문으로 구성되며, 필요에 따라 문법을 축약할 수 있습니다.
- 클로저는 외부 문맥의 값을 캡처할 수 있으며, 이를 통해 상태를 유지하거나 비동기 작업을 처리할 수 있습니다.
- 순환 참조를 피하기 위해 `[weak self]` 또는 `[unowned self]`를 적절히 사용해야 합니다.

---
