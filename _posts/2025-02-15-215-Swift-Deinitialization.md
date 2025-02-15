---
title: 15.Deinitialization
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Deinitialization**
2. **개요**
3. **Deinitializer의 특징**
4. **Deinitializer의 문법**
5. **예제 코드**
6. **주의사항**

## **Deinitialization (역초기화)**

### **개요**
- **Deinitializer**는 클래스 인스턴스가 메모리에서 해제되기 직전에 호출되는 특별한 메서드입니다.
- Swift에서는 자동 메모리 관리(Automatic Reference Counting, ARC)를 통해 메모리를 관리하므로, 대부분의 경우 수동으로 메모리를 해제할 필요가 없습니다.
- 하지만 특정 리소스(예: 파일 핸들, 네트워크 연결 등)를 해제하거나 정리해야 하는 경우 Deinitializer를 사용할 수 있습니다.

---

### **Deinitializer의 특징**
1. **클래스 전용**: Deinitializer는 클래스 타입에만 정의할 수 있습니다. 구조체나 열거형에는 사용할 수 없습니다.
2. **자동 호출**: Deinitializer는 인스턴스가 더 이상 참조되지 않아 ARC에 의해 메모리에서 해제될 때 자동으로 호출됩니다.
3. **파라미터 없음**: Deinitializer는 파라미터를 받지 않습니다.
4. **명시적 호출 불가**: 프로그래머가 직접 호출할 수 없으며, 시스템이 자동으로 관리합니다.

---

### **Deinitializer의 문법**
```swift
deinit {
    // 정리 코드 작성
}
```
- `deinit` 키워드를 사용하여 정의합니다.
- 중괄호 `{}` 안에 필요한 정리 작업을 작성합니다.

---

### **예제 코드**
다음은 Deinitializer를 사용한 간단한 예제입니다:

```swift
class Bank {
    static var coinsInBank = 10_000
    static func distribute(coins: Int) -> Int {
        let coinsToDistribute = min(coins, coinsInBank)
        coinsInBank -= coinsToDistribute
        return coinsToDistribute
    }
    
    static func receive(coins: Int) {
        coinsInBank += coins
    }
}

class Player {
    var coinsInPurse: Int
    
    init(coins: Int) {
        coinsInPurse = Bank.distribute(coins: coins)
    }
    
    func win(coins: Int) {
        coinsInPurse += Bank.distribute(coins: coins)
    }
    
    deinit {
        Bank.receive(coins: coinsInPurse)
        print("Player deinitialized. Returned \(coinsInPurse) coins to the bank.")
    }
}

// Player 인스턴스 생성 및 사용
var playerOne: Player? = Player(coins: 100)
playerOne?.win(coins: 50)

// 인스턴스 해제
playerOne = nil
// 출력: "Player deinitialized. Returned 150 coins to the bank."
```

---

### **설명**
1. **Bank 클래스**:
   - 은행의 코인을 관리하는 클래스입니다.
   - `distribute` 메서드로 코인을 분배하고, `receive` 메서드로 코인을 회수합니다.

2. **Player 클래스**:
   - 플레이어가 소유한 코인을 관리합니다.
   - `init`에서 은행으로부터 코인을 분배받고, `deinit`에서 소유한 코인을 은행에 반환합니다.

3. **Deinitializer 동작**:
   - `playerOne` 변수가 `nil`로 설정되면서 참조 카운트가 0이 되고, ARC에 의해 메모리에서 해제됩니다.
   - 이때 `deinit`이 호출되어 플레이어가 소유한 코인이 은행으로 반환됩니다.

---

### **주의사항**
1. **순환 참조(Circular Reference)**:
   - 두 개 이상의 객체가 서로를 강하게 참조하면 메모리 누수가 발생할 수 있습니다.
   - 이를 방지하기 위해 `weak` 또는 `unowned` 키워드를 사용하여 참조를 약하게 설정하세요.

2. **Deinitializer 호출 순서**:
   - 상속된 클래스의 경우, 자식 클래스의 `deinit`이 먼저 호출되고, 그 후 부모 클래스의 `deinit`이 호출됩니다.

---

### **정리**
Deinitializer는 클래스 인스턴스가 메모리에서 해제되기 전에 필요한 정리 작업을 수행하는 데 사용됩니다. Swift의 ARC 덕분에 대부분의 메모리 관리는 자동으로 처리되지만, 특정 리소스를 명시적으로 해제해야 할 때 유용하게 활용할 수 있습니다.
