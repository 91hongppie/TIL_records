# Generic이란?
- 제네릭이란 타입에 의존하지 않는 범용 코드를 작성할 때 사용한다.
- 제네릭을 사용하면 중복을 피하고, 코드를 유연하게 작성할 수 있다.
- Swift에서 가장 강력한 기능 중 하나로 Swift 표준 라이브러리의 대다수는 제네릭으로 선언되어 있다고 한다.

## 제네릭 함수(Generic Function)
- 인자로 오는 두 Int 타입의 값을 swap하는 함수를 만든다고 해보자
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
	let tempA = a
	a = b
	b = tempA
}
```
- 위 코드는 잘 구현한 것 같다.
- 파라미터 모두 Int형일 경우에는 문제 없이 돌아아겠지만, 파라미터 타입이 Double, String일 경우엔 사용할 수 없다.
- 따라서 만약 Double, String 타입에 대해서 swap 함수를 사용하고 싶다면
```swift
func swapTwoInts(_ a: inout Double, _ b: inout Double) {
	let tempA = a
	a = b
	b = tempA
}

func swapTwoInts(_ a: inout String, _ b: inout String) {
	let tempA = a
	a = b
	b = tempA
}
```
- 이렇게 하나하나 해당 형식에 맞게끔 함수를 오버로딩할 수 있는데 코드 중복이 엄청나다...
- 이럴 때 사용하는 것이 **제네릭**이다.
- 타입에 제한을 두지 않는 코드를 사용하고 싶을 때 쓴다.
```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
	let tempA = a
	a = b
	b = tempA
}
```
- 이런 식으로 사용한다.
- 꺽쇠<>를 이용해서 안에 타입처럼 사용할 이름(T)를 선언해주면 그 뒤로 해당 이름(T)를 타입처럼 사용할 수 있다.
- 여기서 이 T를 Type Parameter라고 부르는데 T라는 새로운 형식이 생성되는 것이 아니라, 실제 함수가 호출될 때 해당 매개변수의 타입으로 대체되는 Placeholder이다.
- 함수 이름 뒤에 꺽쇠로 T를 감싸는 이유는 T는 새로운 형식이 아니라 Placeholder이기 때문에 Swift한테 T는 새로운 타입이 아니라 자리 타입이라고 알려주는 것
- 따라서 이렇게 swapTwoValues라는 함수를 제네릭으로 선언해주면
```swift
var someInt = 1
var anotherInt = 2
swapTwoValues($someInt, $anotherInt) // 함수 호출시 T는 Int

var someString = "Hi"
var anotherString = "Bye"
swapTwoValues($someString, $anotherString) // 함수 호출 시 T는 String
```
- 이렇게 실제 함수를 호출할 때 Type 