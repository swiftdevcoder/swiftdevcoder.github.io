---
title: Error Handling
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**

1. **오류 표현하기 (Representing Errors)**  
2. **오류 던지기 (Throwing Errors)**  
3. **오류 처리하기 (Handling Errors)**  
4. **오류 전파 (Propagating Errors)**  
5. **오류 변환 (Converting Errors to Optional Values)**  
6. **강제 오류 처리 (Forced Try)**  
7. **defer를 사용한 정리 작업 (Using defer for Cleanup)**  
8. **오류 처리의 장점 (Advantages of Error Handling)**

## **Swift의 오류 처리 (Error Handling)**

오류 처리는 프로그램 실행 중 발생할 수 있는 예외 상황을 적절히 처리하는 방법입니다. Swift에서는 오류를 던지고(throw), 잡고(catch), 전파하고(propagate) 처리하는 강력한 메커니즘을 제공합니다.

---

### **1. 오류 표현하기**
Swift에서는 `Error` 프로토콜을 준수하는 타입을 사용하여 오류를 표현합니다. 일반적으로 열거형(enum)을 사용하여 오류 유형을 정의합니다.

```swift
enum FileError: Error {
    case fileNotFound
    case fileCorrupted
    case insufficientPermissions
}
```

- 위의 예시에서 `FileError`는 파일 관련 오류를 나타내는 열거형입니다.
- 각 케이스는 특정 오류 상황을 나타냅니다.

---

### **2. 오류 던지기 (Throwing Errors)**
함수나 메서드에서 오류가 발생할 가능성이 있다면, 해당 함수의 반환 타입 앞에 `throws` 키워드를 추가합니다. 이 함수는 오류를 던질 수 있습니다.

```swift
func readFile(named filename: String) throws -> String {
    if filename.isEmpty {
        throw FileError.fileNotFound
    }
    // 파일 읽기 로직
    return "File content"
}
```

- `throws` 키워드는 함수가 오류를 던질 수 있음을 나타냅니다.
- `throw` 키워드를 사용하여 특정 오류를 던집니다.

---

### **3. 오류 처리하기**
오류가 발생할 수 있는 함수를 호출할 때는 `do-catch` 구문을 사용하여 오류를 처리합니다.

#### **예제: do-catch 사용**
```swift
do {
    let content = try readFile(named: "example.txt")
    print("File content: \(content)")
} catch FileError.fileNotFound {
    print("Error: File not found.")
} catch FileError.fileCorrupted {
    print("Error: File is corrupted.")
} catch {
    print("An unexpected error occurred: \(error).")
}
```

- `try` 키워드는 오류가 발생할 수 있는 코드를 호출할 때 사용합니다.
- `catch` 블록은 발생한 오류를 처리합니다. 특정 오류 유형을 처리하거나, 기본적인 `catch` 블록으로 모든 오류를 처리할 수 있습니다.

---

### **4. 오류 전파 (Propagating Errors)**
함수 내부에서 오류가 발생하면, 이를 호출자에게 전파할 수 있습니다. 호출자는 다시 오류를 처리하거나 더 상위로 전파할 수 있습니다.

#### **예제: 오류 전파**
```swift
func processFile(named filename: String) throws {
    let content = try readFile(named: filename)
    print("Processing content: \(content)")
}
```

- `processFile` 함수는 `readFile` 함수에서 발생한 오류를 호출자에게 전파합니다.
- 호출자는 `try`와 함께 이 함수를 호출해야 합니다.

---

### **5. 오류 변환 (Converting Errors to Optional Values)**
오류를 무시하고 결과를 옵셔널 값으로 변환하려면 `try?`를 사용할 수 있습니다.

#### **예제: try? 사용**
```swift
if let content = try? readFile(named: "example.txt") {
    print("File content: \(content)")
} else {
    print("Failed to read the file.")
}
```

- `try?`는 오류가 발생하면 `nil`을 반환합니다.

---

### **6. 강제 오류 처리 (Forced Try)**
오류가 절대 발생하지 않을 것이라고 확신할 때는 `try!`를 사용할 수 있습니다. 하지만 오류가 발생하면 런타임 오류가 발생합니다.

#### **예제: try! 사용**
```swift
let content = try! readFile(named: "example.txt")
print("File content: \(content)")
```

- `try!`는 신중하게 사용해야 합니다.

---

### **7. defer를 사용한 정리 작업**
`defer` 키워드는 함수가 종료되기 직전에 실행될 코드를 정의합니다. 오류가 발생하더라도 `defer` 블록은 항상 실행됩니다.

#### **예제: defer 사용**
```swift
func openFile(named filename: String) throws {
    print("Opening file...")
    defer {
        print("Closing file...")
    }
    if filename.isEmpty {
        throw FileError.fileNotFound
    }
    print("File opened successfully.")
}
```

- `defer`는 리소스 해제 또는 정리 작업에 유용합니다.

---

### **8. 오류 처리의 장점**
- **안정성**: 예상치 못한 상황에서도 프로그램이 안정적으로 동작하도록 보장합니다.
- **명확성**: 오류 유형과 처리 방식을 명확히 정의할 수 있습니다.
- **유연성**: 다양한 오류 처리 패턴(`do-catch`, `try?`, `try!`)을 지원합니다.

---

### **요약**
Swift의 오류 처리는 다음과 같은 주요 요소로 구성됩니다:
1. `Error` 프로토콜을 준수하는 타입으로 오류를 정의합니다.
2. `throws` 키워드를 사용하여 오류를 던질 수 있는 함수를 정의합니다.
3. `do-catch` 구문을 사용하여 오류를 처리합니다.
4. `try?` 또는 `try!`를 사용하여 간단히 처리하거나 강제로 실행합니다.
5. `defer`를 사용하여 정리 작업을 보장합니다.
