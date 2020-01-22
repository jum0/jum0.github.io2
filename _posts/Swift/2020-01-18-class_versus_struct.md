---
layout: post
title: Swift) Class와 Struct 비교
tags: Swift class struct
categories: Swift
---
## 목차

#### 1. class 와 struct 비교

#### 2. class

#### 3. struct

#### 4. 참고 



## 1. class 와 struct 비교

|                 |          Class          |       Struct        |
| :-------------: | :---------------------: | :-----------------: |
|    **상속**     |          가능           |       불가능        |
|   **초기화**    |          필요           |        선택         |
| **데이터 전달** | Pass(call) by reference | Pass(call) by value |
|    **기타**     | override (상속과 관련)  |      mutating       |



## 2. Class

```swift
// main.swift

let account1 = VIPAccount(name: "jumo", balance: 50000)
let account2 = account1

account1.withdraw10000won()
// 인출금은 10000원, 수수료는 500원, 잔액은 39500원입니다.
// VIP고객으로 수수료 500원이 입금되었습니다. 잔액은 40000원입니다
print(account1.balance) // 40000
print(account2.balance) // 40000
```

```swift
// AccountClass.swift - 부모 클래스(super class)

// struct Accont와 구분하기 위해서 AccountClass를 사용
class AccountClass {
  var name: String
  var balance: Int
  
  init(name: String, balance: String) {
    self.name = name
    self.balance = balance
  }
  
  func withdraw10000won() {
    balance -= 10500
    print("인출금은 10000원, 수수료는 500원, 잔액은 \(balance)원입니다.")
  }
}
```

```swift
// VIPAccount.swift - 자식 클래스(sub class)

class VIPAccount: AccountClass {
  override func withdraw10000won() {
    super.withdraw10000won()
    balance += 500
    print("VIP고객으로 수수료 500원이 입금되었습니다. 잔액은 \(balance)원입니다.")
  }
}
```

- 상속
  
- `class VIPAccount`는 `class AccountClass`를 상속하고 있음. `VIPAccount.swift`에서 `class VIPAccount` 옆에 상속받을 클래스(`AccountClass`)를 씀.
  
- 초기화
  
- `Account.swift`에서 `var name: String`과 같이 프로퍼티의 타입만 적어준 경우 `init` 키워드를 통해 초기화를 해야함. `var name = "jumo"`와 같이 `class` 안의 프로퍼티에 값을 지정한 경우 초기화하지 않아도 됨.
  
- Pass(call) by reference

  - 예를 들어, `account1`이라는 계좌가 `Desktop/jum0.github.io/_post/Swift`에 있다고 가정하고 `let account2 = account1`이라고 했을 때, `account2`에게 `account1` 계좌가 있는 위 주소를 전달하는 것.

  - ```swift
    // main.swift
    
    let account1 = VIPAccount(name: "jumo", balance: 50000)
    let account2 = account1
    
    account1.withdraw10000won()
    // 인출금은 10000원, 수수료는 500원, 잔액은 39500원입니다.
    // VIP고객으로 수수료 500원이 입금되었습니다. 잔액은 40000원입니다
    print(account1.balance) // 40000
    print(account2.balance) // 40000
    ```

    class는 pass(call) by reference이므로 `account1.withdraw10000won()`와 같이 `account1`의 메서드를 실행해도  `account1.balance`와  `account2.balence2`가 같이 바뀜.

- override

  - override 키워드를 통해서 super class의 메서드에 덮어쓰기 가능. super class에 있는 있는 메서드를 사용하려면 `super.메서드명`을 통해서 사용 가능(override func 말고도 sub class 내에서 자유롭게 사용 가능).



## 3. Struct

```swift
// main.swift

var account1 = AccountStruct(name: "jumo", balance: 50000) 
// 초기화 생략하면 AccountStrcut()도 가능
var account2 = account1

account1.withdraw10000won() // 인출금은 10000원, 수수료는 500원, 잔액은 39500원입니다.
print(account1.balance) // 39500
print(account2.balance) // 50000
```

```swift
// AccountStruct.swift

// class Accont와 구분하기 위해서 AccountStruct를 사용
struct AccountStruct {
  var name: String
  var balance: Int
    
  
  init(name: String, balance: Int) {
    self.name = name
    self.balance = balance
  }

  mutating func withdraw10000won() {
    balance -= 10500
    print("인출금은 10000원, 수수료는 500원, 잔액은 \(balance)원입니다.")
  }
}
```

- 상속 불가능
- 초기화
  
- 초기화하는 것은 선택 (`init` 키워드).
  
- Pass(call) by value

  - ```swift
    // main.swift
    
    var account1 = AccountStruct(name: "jumo", balance: 50000) 
    // 초기화 생략하면 AccountStrcut()도 가능
    var account2 = account1
    
    account1.withdraw10000won() // 인출금은 10000원, 수수료는 500원, 잔액은 39500원입니다.
    print(account1.balance) // 39500
    print(account2.balance) // 50000
    ```

  - class와 다르게 `var account2 = account1`는 같은 `account1`이 가리키는 인스턴스(객체)를 참조하는 것이 아닌 새로운 객체 생성을 의미하므로 `account1.withdraw10000won()` 코드 실행 후, `account1.balance`와 `account2.balance`는 다름.

- mutating
  - struct 내의 메서드 중에서 프로퍼티에 영향을 주면(update) `mutating` 키워드를 붙임.
  - `AccountStruct.swift`에서 `withdraw10000won` 메서드에 `mutating` 키워드를 붙는 이유는 struct 내의 프로퍼티(`balance`)에 영향을 주는 메서드이기 때문.



## 4. 참고

- 초기화 할 때, parameter를 변경할 수 있음

  - ```swift
    struct AccountStruct {
      var name: String
      var balance: Int
        
      // parameter 변경
      init(n: String, b: Int) {
        self.name = n
        self.balance = b
      }
    
      mutating func withdraw10000won() {
        balance -= 10500
        print("인출금은 10000원, 수수료는 500원, 잔액은 \(balance)원입니다.")
      }
    }
    ```

  - ```swift
    var account1 = Account(n: "jumo", b: 50000)
    ```

- Apple에서는 Default로 struct 사용하기를 권장
  
  - https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes





혹시 잘못된 부분이 있으면 말씀해주세요! 감사합니다:)

