---
title: Type Casting
layout: single
classes: wide
category: 아이폰앱 개발
tags:
    - swift
---

## **목차**
1. **Type Casting이란?**
2. **Type Checking (`is` 연산자)**
3. **Downcasting (`as?`, `as!` 연산자)**
4. **Any와 AnyObject의 Type Casting**
5. **Type Casting과 Switch 문**
6. **요약**

## **1. Type Casting이란?**
- **Type casting**은 인스턴스의 타입을 확인하거나, 특정 클래스나 서브클래스의 인스턴스를 참조할 수 있도록 타입을 변환하는 과정입니다.
- Swift에서는 `is`와 `as` 연산자를 사용하여 type casting을 수행합니다.

---

## **2. Type Checking (`is` 연산자)**
- `is` 연산자는 인스턴스가 특정 클래스의 인스턴스인지 또는 특정 클래스의 서브클래스인지 확인합니다.
- 예시:
  ```swift
  class Media {
      var name: String
      init(name: String) {
          self.name = name
      }
  }

  class Movie: Media {
      var director: String
      init(name: String, director: String) {
          self.director = director
          super.init(name: name)
      }
  }

  class Song: Media {
      var artist: String
      init(name: String, artist: String) {
          self.artist = artist
          super.init(name: name)
      }
  }

  let library: [Media] = [
      Movie(name: "Inception", director: "Christopher Nolan"),
      Song(name: "Bohemian Rhapsody", artist: "Queen")
  ]

  for item in library {
      if item is Movie {
          print("Movie: \(item.name)")
      } else if item is Song {
          print("Song: \(item.name)")
      }
  }
  ```
  - 출력:
    ```
    Movie: Inception
    Song: Bohemian Rhapsody
    ```

---

## **3. Downcasting (`as?`, `as!` 연산자)**
- **Downcasting**은 상위 클래스 타입의 인스턴스를 하위 클래스 타입으로 변환하는 작업입니다.
- 안전한 downcasting을 위해 `as?`를 사용하며, 실패 가능성을 처리할 수 있습니다.
- 강제 downcasting인 `as!`는 변환이 실패하면 런타임 오류가 발생하므로 신중히 사용해야 합니다.

### **예시:**
```swift
for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.name), directed by \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}
```
- 출력:
  ```
  Movie: Inception, directed by Christopher Nolan
  Song: Bohemian Rhapsody, by Queen
  ```

---

## **4. Any와 AnyObject의 Type Casting**
Swift에서는 두 가지 특별한 타입이 존재합니다:
- **Any**: 모든 타입(클래스, 구조체, 열거형, 함수 등)을 나타낼 수 있는 타입.
- **AnyObject**: 클래스 타입만 나타낼 수 있는 타입.

### **예시:**
```swift
let someObjects: [AnyObject] = [
    Movie(name: "Inception", director: "Christopher Nolan"),
    Song(name: "Bohemian Rhapsody", artist: "Queen") as AnyObject
]

for object in someObjects {
    if let movie = object as? Movie {
        print("Movie: \(movie.name), directed by \(movie.director)")
    } else if let song = object as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}
```

---

## **5. Type Casting과 Switch 문**
- `switch` 문을 사용하여 다양한 타입을 효율적으로 처리할 수 있습니다.
- `case` 내부에서 타입 캐스팅을 동시에 수행할 수 있습니다.

### **예시:**
```swift
for item in library {
    switch item {
    case let movie as Movie:
        print("Movie: \(movie.name), directed by \(movie.director)")
    case let song as Song:
        print("Song: \(song.name), by \(song.artist)")
    default:
        print("Unknown media type")
    }
}
```

---

## **6. 요약**
- **`is` 연산자**: 인스턴스의 타입을 확인합니다.
- **`as?` 연산자**: 안전하게 타입을 변환합니다(옵셔널 반환).
- **`as!` 연산자**: 강제로 타입을 변환합니다(실패 시 런타임 오류).
- **`Any`와 `AnyObject`**: 다양한 타입을 처리할 때 유용합니다.
- **`switch` 문**: 복잡한 타입 캐스팅 로직을 간결하게 작성할 수 있습니다.

