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
swapTwoValues(&someInt, &anotherInt) // 함수 호출시 T는 Int

var someString = "Hi"
var anotherString = "Bye"
swapTwoValues(&someString, &anotherString) // 함수 호출 시 T는 String
```
- 이렇게 실제 함수를 호출할 때 Type Parameter인 T의 타입이 결정되는 것
- 하지만 여기서 파라미터 a, b 모두 같은 타입 파라미터인 T로 선언되어 있기 때문에
```swift
swapTwoValuee(&someInt, &anotherString)
```
- 서로 다른 타입을 파라미터로 전달하면, 첫 번째 someInt를 통해 타입파라미터 T가 Int로 결정됐기 때문에, 두 번째 파라미터인 anotherString의 타입이 Int가 아니라며 에러가 난다.
- 똑같은 내용의 함수를 오버로딩 할 필요없이 제네릭을 사용하면 된다. 
- 따라서 코드 중복을 피하고 유연하게 코드를 작성할 수 있다.

- 타입 파라미터는 굳이 T가 아니어도 된다.
- 여러개를 comma(,)를 이용해서 선언할 수도 있다.

```swift
func swapTwoValues<One, Two> {...}
```
- 보통 타입 파라미터 이름을 선언할 땐 가독성을 위해 T나 V 같은 단일 문자, 혹은 Upper Camel Case를 사용한다고 한다.

## 제네릭 타입 (Generic Type)
- 제네릭을 이용한 함수를 제네릭 함수라고 한다.
- 제네릭을 이용한 타입은 제네릭 타입이라고 함
	- 구조체, 클래스, 열거형 타입에 선언이 가능하다.

```swift
struct Stack<T> {
	let items: [T] = []

	mutating func push(_ item: T) { ... }
	mutating func pop() -> T { ... }
}
```
- 이렇게 제네릭 타입으로 Stack을 선언할 수 있다. ( 클래스, 열거형도 가능 )
- 제네릭 타입의 인스턴스를 생성할 때는 어떻게 해야할까?
```swift
let stack1: Stack<Int> = .init()
let stack2 = Stack<Int>.init()
```
- 이렇게 제네릭 타입을 선언할 땐, 선언과 마찬가지로 <>를 통해 어떤 타입으로 사용할 것인지를 명시해주어야 함
```swift
let array1: Array<Int> = .init()
let array2 = Array<Int>.init()
```
- 배열도 제네릭 타입이랑 똑같이 인스턴스를 생성한다.
- 왜냐하면 Swift에선 Array가 제네릭 타입이기 때문이다.

# 타입 제약 (Type Constraints)
- 제네릭 함수와 타입을 사용할 때 특정 클래스의 하위 클래스나, 특정 프로토콜을 준수하는 타입만 받을 수 있게 제약을 둘 수 있다.
## 프로토콜 제약
- 이번엔 파라미터 두 개를 받아서 두 값이 같으면 true, 다르면 false를 반환하는 함수를 제네릭으로 선언하려고 한다.
```swift
func isSameValues<T>(_ a: T, _ b: T) -> Bool {
	return a == b
}
```
- 위에처럼 하면 될 것 같지만, 에러가 발생한다.
- == 연산자는, a와 b의 타입이 Equatable이란 프로토콜을 준수할 때만 사용할 수 있음
- 우리가 T라고 선언한 타입 파라미터는, a, b가 Equatable 프로토콜을 준수하는 타입일 수도, 아닐수도 있는데 아닐수도 있기 때문에 == 연산자를 사용하지 못하는 것
```swift
func isSameValues<T: Equatable>(_ a: T, _ b: T) -> Bool {
	return a == b
}
```
- 위처럼 타입 파라미터에 T: Equatable 이런 식으로 제약을 줄 수 있다.
- 이렇게 하면, isSameValues란 함수에 들어올 수 있는 파라미터는 Equatable이란 프로토콜을 준수하는 파라미터만 받을 수 있음
## 클래스 제약
- 클래스 제약 같은 경우엔 프로토콜 제약과 같지만, 해당 자리에 프로토콜이 아닌 클래스 이름이 오는 것이다.
```swift
class Bird { }
class Human { }
class Teacher: Human { }

func printName<T: Human>(_ a: T) { }
```

- 이렇게 T: Human 이런 식으로 클래스 이름을 써주면
```swift
let bird = Bird.init()
let human = Human.init()
let teacher = Teacher.init()

printName(bird)
printName(human)
printName(teacher)
```
- Human클래스 인스턴스인 human과 Human클래스를 상속 받은 teacher은 printName이란 제네릭 함수를 실행시킬 수 있지만, Human 클래스의 서브 클래스가 아닌 bird 클래스는 실행할 수 없다.
- 이런 식으로 클래스로 제약을 주는 것도 가능하다.

# 제네릭 확장하기
- 만약 제네릭 타입인 Array를 내가 확장하고 싶다면 어떻게 해야할까?
```swift
extension Array {
	mutating func pop() -> Element {
		return self.removeLast()
	}
}
```
- 만약 제네릭 타입을 확장하면서 타입 파라미터를 사용할 경우, 실제 Array 구현부에서 타입 파라미터가 Element이기 때문에 Element로 사용해야 함
- 확장에서 새로운 제네릭을 선언하거나, 다른 타입 파라미터를 사용하면 안된다.
- where을 통해 확장 또는 제약을 줄 수 있다
```swift
extension Array where Element: FixedWidthInteger {
	mutating func pop() -> Element { return self.removeLast() }
}
```
- 이렇게, 타입 파라미터 Element가 FixedWidthInteger라는 프로토콜을 준수해야 한다라는 제약을 주면
```swift
let nums = [1, 2, 3]
let strs = ["a", "b", "c"]

nums.pop() // 0
strs.pop() // X
```
- FixedWidthInteger 프로토콜을 준수하는 Array\<Int> 형인 nums는 extension에서 구현된 pop이란 메서드를 사용할 수 있다
- 하지마, FixedWidthInteger 프로토콜을 준수하지않는 Array\<String> 형인 strs는 extension에서 구현된 pop이란 메서드를 사용할 수 없다.

# 제네릭 함수와 오버로딩
- 제네릭은 보통 타입에 관계없이 동일하게 실행되지만, 만약 특정 타입일 경우 제네릭말고 다른 함수로 구현하고 싶다면 <span style='color: red'>제네릭 함수를 오버로딩</span> 하면 된다.
```swift
func swapValues<T>(_ a: inout T, _ b: inout T) {
	print("generic func")
	let tempA = a
	a = b
	b = tempA												
}

func swapValues(_ a: inout Int, _ b: inout Int) {
	print("specialized func")
	let tempA = a
	a = b
	b = tempA												
}
```
- 이렇게 할 경우 타입이 지정된 함수가 제네릭 함수보다 우선순위가 높아서
```swift
var a = 1
var b = 2
swapValues(&a, &b) // specialized func

var c = "Hi"
var d = "Kyu~"
swapValues(&c, &d) // generic func
```
- Int 타입으로 swapValues를 실행할 경우, 타입이 지정된 함수가 실행되고, String 타입으로 swapValue를 실행할 경우, 제네릭 함수가 실행된다.

- [[Protocol]]에서 