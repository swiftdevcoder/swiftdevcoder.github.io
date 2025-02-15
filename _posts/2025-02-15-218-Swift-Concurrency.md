---
title: 18.Concurrency
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**

1. **동시성의 기본 개념**
2. **Swift 동시성의 핵심 구성 요소**
3. **동시성의 장점**
4. **주의사항**
5. **실무에서의 활용**

## **Swift 동시성(Concurrency) 학습 요약**

Swift의 동시성 모델은 비동기 작업과 병렬 처리를 쉽게 작성하고 관리할 수 있도록 설계되었습니다. 이를 통해 애플리케이션의 성능을 향상시키고, 사용자 경험을 원활하게 유지할 수 있습니다. 아래는 주요 개념과 기능을 정리한 내용입니다.

---

### **1. 동시성의 기본 개념**
- **비동기 작업(Asynchronous Tasks)**: 특정 작업이 완료될 때까지 기다리는 동안 다른 작업을 수행할 수 있는 방식입니다.
- **병렬 처리(Parallelism)**: 여러 작업을 동시에 실행하여 처리 속도를 높이는 방식입니다.
- **스레드(Thread)**: 운영 체제에서 제공하는 실행 단위로, Swift에서는 직접 스레드를 관리하지 않고 고수준 추상화를 사용합니다.

---

### **2. Swift 동시성의 핵심 구성 요소**

#### **(1) `async`와 `await`**
- **`async`**: 함수 또는 메서드가 비동기적으로 실행됨을 나타냅니다.
- **`await`**: 비동기 함수의 결과를 기다리는 키워드입니다. `await`은 비동기 작업이 완료될 때까지 현재 코드의 실행을 일시 중단합니다.
  
**예시:**
```swift
func fetchData() async throws -> Data {
    let url = URL(string: "https://example.com/data")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}
```

- 위 코드에서 `await`은 네트워크 요청이 완료될 때까지 기다립니다.

---

#### **(2) Task와 Task Group**
- **Task**: 비동기 작업을 실행하는 단위입니다. 독립적으로 실행되며, 필요에 따라 취소할 수 있습니다.
- **Task Group**: 여러 개의 비동기 작업을 그룹화하여 관리할 수 있습니다.

**예시:**
```swift
Task {
    do {
        let data = try await fetchData()
        print("데이터 로드 성공: \(data)")
    } catch {
        print("에러 발생: \(error)")
    }
}
```

---

#### **(3) Actor**
- **Actor**: 데이터 경쟁(Data Race)을 방지하기 위해 설계된 동시성 모델입니다. Actor 내부의 상태는 한 번에 하나의 작업만 접근할 수 있습니다.
  
**예시:**
```swift
actor Counter {
    private var count = 0
    
    func increment() {
        count += 1
    }
    
    func getCount() -> Int {
        return count
    }
}

let counter = Counter()
Task {
    await counter.increment()
    print(await counter.getCount()) // 출력: 1
}
```

- Actor는 스레드 안전성을 보장하며, 상태 변경 시 충돌을 방지합니다.

---

#### **(4) AsyncSequence**
- **AsyncSequence**: 비동기적으로 값을 생성하는 시퀀스입니다. 일반적인 `for-in` 루프처럼 사용할 수 있습니다.
  
**예시:**
```swift
import Foundation

let url = URL(string: "https://example.com/stream")!
let stream = URLSession.shared.bytes(from: url)

Task {
    for try await byte in stream {
        print(byte)
    }
}
```

---

### **3. 동시성의 장점**
1. **코드 간결성**: `async/await`을 사용하면 콜백 지옥(Callback Hell)을 피할 수 있습니다.
2. **스레드 안전성**: Actor와 같은 도구를 통해 데이터 경쟁을 방지할 수 있습니다.
3. **성능 향상**: 비동기 작업을 통해 애플리케이션이 더 효율적으로 리소스를 활용할 수 있습니다.

---

### **4. 주의사항**
- **에러 처리**: 비동기 함수는 `throws`를 사용하여 에러를 던질 수 있으므로, 적절한 에러 처리가 필요합니다.
- **작업 취소**: `Task`는 취소될 수 있으므로, 작업이 취소되었는지 확인하고 적절히 대응해야 합니다.
  
**예시:**
```swift
Task {
    try? await Task.sleep(nanoseconds: 1_000_000_000)
    if Task.isCancelled {
        print("작업이 취소되었습니다.")
        return
    }
    print("작업 완료")
}
```

---

### **5. 실무에서의 활용**
- **네트워크 요청**: API 호출과 같은 네트워크 작업은 비동기적으로 처리해야 합니다.
- **파일 I/O**: 파일 읽기/쓰기는 시간이 걸릴 수 있으므로 비동기 처리가 적합합니다.
- **UI 업데이트**: UI 관련 작업은 메인 스레드에서 실행되어야 하며, 비동기 작업 후 메인 스레드로 전환해야 합니다.

**예시:**
```swift
Task {
    let data = try await fetchData()
    await MainActor.run {
        updateUI(with: data)
    }
}
```

