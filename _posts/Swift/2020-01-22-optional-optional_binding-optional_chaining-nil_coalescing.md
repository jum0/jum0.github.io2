---
layout: post
title: Swift) Optionals / nil / Forced Unwrapping / Optional Binding / Optional Chaining / Nil Coalescing Operator 정리
tags: Swift optionals nil forced-unwrapping optional-binding optional-chaining Xcode Nil-Coalescing-Operator 스위프트
categories: Swift
---
## 참조

THE SWIFT PROGRAMMING LANGUAGE SWIFT 5.1 참조

https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html



## 목차

#### 1. Optionals

#### 2. nil

#### 3. Forced Unwrapping

#### 4. Optional Binding

#### 5. Optional Chaining

#### 6. Nil Coalescing Operator



## 1. Optionals

- 값이 존재할 수도, 존재하지 않을 수도 있다는 두 가지 가능성을 의미.

  - 값이 존재하여, 값에 접근하기 위해 optional을 unwrap 할 수도 있고, 값이 없을 수도 있음.

- `?` 를 사용하여 나타냄.

  ```swift
  let number: Int?
  // 상수 number에 Int 값이 존재할 수도, 존재하지 않을 수도 있다는 것을 의미.
  ```

- `Int?`과 `Int`는 다름.

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber는 "Int?" 타입이나 "optional Int"로 추정됨.
```

> initializer가 초기화하는 것을 실패할 수도 있기 때문에, print 해보면 Int 말고 optional Int로 반환함. Optional Int는 Int?로 표시되며 Int와는 다르다. 



## 2. nil

- Optional 변수에 nil을 할당함으로써 값이 없는 상태를 나타냄.

  ```swift
  var serverResponseCode: Int? = 404
  // serverResponseCode는 404의 Int 값을 가지고 있음.
  serverResponseCode = nil
  // serverResponseCode는 현재 값을 가지고 있지 않음.
  ```

  > nil은 optional이 아닌 상수나 변수에 사용할 수 없음.

- 기본 값을 설정하지 않고 optional 변수를 선언하면, 그 변수는 자동으로 `nil`이 할당됨.

  ```swift
  var surveyAnswer: String?
  // surveyAnswer에 자동으로 nil이 할당됨.
  ```



## 3. Forced Unwrapping

- optional 값을 강제로 꺼내오는 것.

  - optional이 확실하게 값을 가지고 있다고 가정할 때 사용.

- `!` 를 사용.

- 성공적으로 Build 되어도 오류가 발생할 수 있으므로 사용하는 것을 지양하며, 보통 `If` 구문과 같이 사용됨.

  ```swift
  if convertedNumber != nil {
    print("covertedNumber가 integer \(convertedNumber!) 값을 가지고 있다.")
  }
  // Print: convertedNumber가 integer 123 값을 가지고 있다.
  ```



## 4. Optional Binding

- 값을 가지고 있는지 없는지 알고자 할 때 사용.

  - 값이 있다면 상수나 변수에 할당하여 그 값을 사용하기 위해서 쓰임.

- `if let` (또는 `if var`) 구문을 통해서 사용.

  ```swift
  // 1. Optionals 예제에서 쓰인 변수 사용.
  
  if let actualNumber = Int(possibleNumber) {
    print("String \"\(possibleNumber)\"는 integer \(actualNumber) 값을 가진다.")
  } else {
    print("String \"\(possibleNumber)\"는 integer로 변환될 수 없다.")
  }
  // Print: String "123"는 integer 123 값을 가진다.
  ```

- `,`를 사용하여 여러 optional과 조건을 동시에 확인 가능.

  ```swift
  // 예시 1.
  if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
      print("\(firstNumber) < \(secondNumber) < 100")
  }
  // Print: "4 < 42 < 100"
  
  // 예시 2.
  if let firstNumber = Int("4") {
      if let secondNumber = Int("42") {
          if firstNumber < secondNumber && secondNumber < 100 {
              print("\(firstNumber) < \(secondNumber) < 100")
          }
      }
  }
  // Print: "4 < 42 < 100"
  ```

  

## 5. Optional Chaining

- 하위 프로퍼티에 optional 값이 있는지 연속적으로 확인하는 방식.
  - 중간에 하나라도 nil이 발견된다면 nil을 반환함.

```swift
class Person {
  var residence: Residence?
}

class Residence {
  var numberOfRooms = 1
}

let jumo = Person()
```

> residence 변수가 Residence 클래스를 상속받고 있는데, Residence 클래스의 type이 optional이므로 Person 타입의 인스턴스(jumo)가 만들어졌을 때,  변수 residence의 초기값은 nil이 됨(초기값을 설정하지 않고 optional 변수를 선언하므로).

```swift
if let roomCount = jumo.residence?.numberOfRooms {
  print("jumo는 객실 \(roomCount)를 가지고 있습니다.")
} else {
  print("객실의 수를 찾을 수 없습니다.")
}
// Print: 객실의 수를 찾을 수 없습니다.
```

> 위와 같은 결과가 나오는 이유는 인스턴스 jumo의 프로퍼티 residence가 nil이므로, `if`문에서 `jumo.residence?` 그 다음 확인할 프로퍼티 `numberOfRooms`로 넘어가지 않아, `else`문을 수행하게 되기 때문에. `if`문을 실행시키기 위해서는, `let jumo = Person()` 코드 다음에 `jumo.residence = Residence()` 코드를 추가하면 됨.



## 6. Nil Coalescing Operator

- nil-coalescing operator을 삼항다항식으로 나타내면 아래의 코드와 같은 의미를 지님.

  ```swift
  a != nil ? a! : b
  // a의 값이 nil이 아니면 a에 a를 forced-unwrap한 값(a!)을 넣고, nil이라면 a에 b의 값을 할당함.
  ```

- `??` 사용.

```swift
let defaultColorName = "red"
var userDefinedColorName: String? // 초기값 nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName이 nil이므로, colorNameToUse 변수에 defaultColorName의 값인 "red"를 할당함.
```

```swift
userDefinedColorName = "green"
colorNameToUse = userDefinedColorNmae ?? defaultColorName
// userDefinedColorName의 값이 nil이 아니므로 colorNameToUse에 할당함.
// colorNameToUse의 값은 "green"이 됨.
```



혹시 잘못된 부분이 있으면 말씀해주세요! 감사합니다:)

