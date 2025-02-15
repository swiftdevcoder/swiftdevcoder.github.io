---
title: Enumerations
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Enumerations(열거형)란?**
2. **열거형의 기본 사용법**
3. **열거형의 고급 기능**
4. **열거형의 장점**


### **1. Enumerations(열거형)란?**
- **정의**: 열거형은 관련된 값들의 그룹을 하나의 타입으로 정의하는 방법입니다.
- **목적**: 코드의 가독성과 안전성을 높이며, 특정한 값만 허용하도록 제한할 수 있습니다.
- **예시**:
  ```swift
  enum CompassPoint {
      case north
      case south
      case east
      case west
  }
  ```
  위 코드는 네 가지 방향(`north`, `south`, `east`, `west`)을 정의한 열거형입니다.

---

### **2. 열거형의 기본 사용법**
#### **2.1. 열거형 선언 및 사용**
- 열거형은 `enum` 키워드로 선언하며, 각 케이스는 `case` 키워드로 정의합니다.
- 사용 시 변수나 상수에 값을 할당할 수 있습니다.
  ```swift
  var direction: CompassPoint = .north
  print(direction) // 출력: north
  ```

#### **2.2. 다중 케이스 정의**
- 여러 케이스를 한 줄에 나열할 수 있습니다.
  ```swift
  enum Planet {
      case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
  }
  ```

#### **2.3. Switch 문과 함께 사용**
- 열거형은 `switch` 문과 함께 사용하면 모든 케이스를 처리할 수 있습니다.
  ```swift
  switch direction {
  case .north:
      print("북쪽으로 이동")
  case .south:
      print("남쪽으로 이동")
  case .east:
      print("동쪽으로 이동")
  case .west:
      print("서쪽으로 이동")
  }
  ```

---

### **3. 열거형의 고급 기능**
#### **3.1. Associated Values(연관 값)**
- 각 케이스에 추가적인 데이터를 저장할 수 있습니다.
- 예시:
  ```swift
  enum Barcode {
      case upc(Int, Int, Int, Int)
      case qrCode(String)
  }

  var productBarcode = Barcode.upc(8, 85909, 51226, 3)
  productBarcode = .qrCode("ABCD1234")

  switch productBarcode {
  case .upc(let numberSystem, let manufacturer, let product, let check):
      print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
  case .qrCode(let code):
      print("QR Code: \(code)")
  }
  ```

#### **3.2. Raw Values(원시 값)**
- 열거형의 각 케이스에 기본값(원시 값)을 할당할 수 있습니다.
- 원시 값은 자동으로 증가하거나 직접 지정할 수 있습니다.
  ```swift
  enum ASCIIControlCharacter: Character {
      case tab = "\t"
      case lineFeed = "\n"
      case carriageReturn = "\r"
  }

  let newline = ASCIIControlCharacter.lineFeed.rawValue
  print(newline) // 출력: \n
  ```

#### **3.3. Recursive Enumerations(재귀 열거형)**
- 열거형 내부에서 자기 자신을 참조할 수 있는 특별한 형태입니다.
- 재귀 열거형은 `indirect` 키워드를 사용합니다.
  ```swift
  indirect enum ArithmeticExpression {
      case number(Int)
      case addition(ArithmeticExpression, ArithmeticExpression)
      case multiplication(ArithmeticExpression, ArithmeticExpression)
  }

  let five = ArithmeticExpression.number(5)
  let four = ArithmeticExpression.number(4)
  let sum = ArithmeticExpression.addition(five, four)
  ```

---

### **4. 열거형의 장점**
1. **타입 안전성**: 잘못된 값을 사용하지 않도록 보장합니다.
2. **코드 가독성**: 의미 있는 이름을 사용하여 코드를 이해하기 쉽게 만듭니다.
3. **유지보수 용이성**: 새로운 케이스를 추가하거나 수정하기 쉽습니다.

---

### **5. 실전 예제**
아래는 열거형을 활용한 간단한 예제입니다.
```swift
enum TrafficLight {
    case red, yellow, green
}

func handleTrafficLight(_ light: TrafficLight) {
    switch light {
    case .red:
        print("정지하세요.")
    case .yellow:
        print("준비하세요.")
    case .green:
        print("출발하세요.")
    }
}

let currentLight = TrafficLight.red
handleTrafficLight(currentLight) // 출력: 정지하세요.
```

