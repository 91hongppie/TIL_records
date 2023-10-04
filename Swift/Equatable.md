- Protocol
- A type that can be compared for value equality.
	- 값이 동일한지 어떤지를 비교 할수있는 타입
- Equatable 프로토콜을 준수하는 타입은 등호 연산자 (\==) 또는 같지않음 연산자(!=)를 사용하여 동등성을 비교할 수 있다.
- Swift 표준 라이브러리의 대부분 기본 데이터타입은 Equatable을 따른다.
- Equatable 프로토콜은 어떤 "타입"이 채택할 수 있다.
	- 타입에는 클래스, 구조체, enum 등이 있다.
- Double, Bool 등 다른 기본적인 데이터타입도 Equatable을 따르고 있다.
```swift
var some = 1
var other = 2

if some == other {
	// code
} else {
	// code
}
```
- 위 코드는 Int지만, String, Double, Bool, Float에 다 적용이 된다.
- 위 타입 모두가 Equatable이라는 프로토콜을 따르고 있기 때문이다.

- 아주 복잡한 클래스나 구조체를 만들었다. <- 얘네도 하나의 타입이다.
- 우리가 이 클래스/구조체의 인스턴스끼리 비교를 하고싶다.
- 그럴때 Xcode는 얘네가 같은지 다른지 모른다.
```swift
class A {
	var aNum: Int
	init(_ aNum: Int) {
		self.aNum = aNum
	}
}


if A(1) == A(2) { // error!
	// code
}
```
-  위 코드에서 Xcode는 A(1)과 A(2)가 같은지 모른다.
- A(1).aNum == A(2).aNum은 알 수 있다. aNum이 Int 타입이기 때문에
- 여기서 A(1) == A(2) 비교를 원한다면, 이 때 Equatable이 필요하다.
- 클래스 A는 Equatable을 채택하고 준수함으로서 동일한지 동일하지 않은지 판별이 가능해지는 것이다.
- 