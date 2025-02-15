---
title: Nexted Type
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **중첩 타입의 기본 개념**
2. **중첩 타입의 장점**
3. **중첩 타입의 접근**
4. **중첩 타입의 활용 예시**
5. **중첩 타입의 제한 사항**
6. **중첩 타입의 실제 활용**

## **중첩 타입 (Nested Types)**

Swift에서는 타입(클래스, 구조체, 열거형 등) 안에 다른 타입을 정의할 수 있습니다. 이를 **중첩 타입**이라고 합니다. 중첩 타입은 코드를 더 명확하고 직관적으로 구성하는 데 유용합니다. 특히 특정 타입 내부에서만 사용되는 보조 타입을 정의할 때 적합합니다.

### **1. 중첩 타입의 기본 개념**
- **중첩 타입**은 클래스, 구조체, 또는 열거형 안에 정의된 타입입니다.
- 중첩 타입은 외부에서 직접 접근할 수 없으며, 해당 타입의 인스턴스나 메서드 내에서만 사용됩니다.
- 중첩 타입은 코드의 가독성을 높이고 관련된 타입을 논리적으로 그룹화하는 데 도움이 됩니다.

```swift
struct BlackjackCard {
    // 중첩된 열거형
    enum Suit: Character {
        case spades = "♠", hearts = "♥", diamonds = "♦", clubs = "♣"
    }

    // 중첩된 구조체
    struct Rank {
        var value: Int
        var description: String {
            switch value {
            case 1:
                return "Ace"
            case 11:
                return "Jack"
            case 12:
                return "Queen"
            case 13:
                return "King"
            default:
                return String(value)
            }
        }
    }

    // 속성
    var rank: Rank
    var suit: Suit
}
```

위 예제에서는 `BlackjackCard`라는 구조체 안에 `Suit` 열거형과 `Rank` 구조체가 중첩되어 정의되었습니다.

---

### **2. 중첩 타입의 장점**
- **범위 제한**: 중첩 타입은 외부에서 직접 접근할 필요가 없는 경우에 유용합니다. 즉, 특정 타입 내부에서만 사용될 때 이를 캡슐화할 수 있습니다.
- **코드 조직화**: 관련된 타입들을 논리적으로 그룹화하여 코드의 구조를 명확하게 만듭니다.
- **명확성 향상**: 중첩 타입을 통해 타입 간의 관계를 더 명확히 표현할 수 있습니다.

---

### **3. 중첩 타입의 접근**
중첩 타입은 바깥쪽 타입의 이름을 통해 접근할 수 있습니다. 예를 들어:

```swift
let heartsSymbol = BlackjackCard.Suit.hearts.rawValue
print(heartsSymbol) // 출력: ♥
```

위 코드에서 `Suit` 열거형은 `BlackjackCard` 구조체 내부에 중첩되어 있으므로, `BlackjackCard.Suit`로 접근해야 합니다.

---

### **4. 중첩 타입의 활용 예시**
아래는 중첩 타입을 활용한 실전 예제입니다. 이 예제는 블랙잭 카드의 계산을 모델링합니다.

```swift
struct BlackjackCard {
    // 중첩된 열거형
    enum Suit: Character {
        case spades = "♠", hearts = "♥", diamonds = "♦", clubs = "♣"
    }

    // 중첩된 구조체
    struct Rank {
        var value: Int
        var description: String {
            switch value {
            case 1:
                return "Ace"
            case 11:
                return "Jack"
            case 12:
                return "Queen"
            case 13:
                return "King"
            default:
                return String(value)
            }
        }
    }

    // 속성
    var rank: Rank
    var suit: Suit

    // 메서드
    func description() -> String {
        return "\(rank.description) of \(suit.rawValue)"
    }
}

// 사용 예시
let aceOfSpades = BlackjackCard(rank: BlackjackCard.Rank(value: 1), suit: .spades)
print(aceOfSpades.description()) // 출력: Ace of ♠
```

---

### **5. 중첩 타입의 제한 사항**
- 중첩 타입은 바깥쪽 타입의 인스턴스 없이도 사용할 수 있습니다. 하지만 중첩 타입이 비중첩 상태라면 외부에서 직접 접근할 수 없습니다.
- 너무 많은 중첩은 코드의 복잡성을 증가시킬 수 있으므로, 필요한 경우에만 사용하는 것이 좋습니다.

---

### **6. 중첩 타입의 실제 활용**
중첩 타입은 다음과 같은 상황에서 유용합니다:
- **특정 타입 내부에서만 사용되는 보조 타입**을 정의할 때.
- **타입 간의 관계를 명확히 표현**하고 싶을 때.
- **코드의 가독성과 유지보수성을 높이고 싶을 때**.

예를 들어, 네트워크 요청과 응답을 처리하는 클래스에서 요청 타입과 응답 타입을 중첩하여 정의할 수 있습니다.
