# POP 탄생 배경
- 일반적으로 OOP에서 클래스의 상속 개념을 통해 공통 기능들을 모듈화하여 사용할 수 있었으나, 구조체 혹은 열거형의 경우에는 상속이 불가하기에 같은 타입에 대해서 공통적인 기능 구현을 위해서는 다른 방법을 이용해야 한다.
- 이를 해결하기 위한 방법이 Apple WWDC15(Swift 2)에서 Extension이 발표되었다
- Protocol(청사진)을 구현하고 Extension으로 해당 프로토콜의 기능을 확장하는 형태로 사용한다.
- 이를 프로토콜 초기 구현 (Protocol Default Implementation)이라고 표현한다.
# POP의 장점
- 코드의 중복을 최소화 할 수 있다.
- 가볍고 안전하다
	- 상속과 달리 필요한 것만 골라서 쓸 수 있다.
	- 상속의 경우, 참조 타입이므로 참조 추적을 위한 비용이 많이 발생하기 때문에 속도 측면에서 다소 느리다.
- 값 타입의 상속 효과
	- 공통된 기능을 쉽게 구현할 수 있다.
- 수평적인 확장 기능
	- Class는 하나의 상속만 가능하고 수직적인 구조가 나타나지만 Protocol을 이용하면 수평적인 확장이 가능하다.
- 제네릭의 활용
	- 예를들어, Swift의 Array의 경우 데이터 타입의 관계없이 만들수 있고 이들 모두가 그에 따른 메서드를 사용할 수 있다.
# [[Protocol]]
- 프로토콜은 특정 기능 수행에 필수적인 요소를 정의한 청사진(blueprint)이다.
- 프로토콜을 만족시키는 타입을 프로토콜을 따른다(conform)고 말한다.
- 프로토콜에 필수 구현을 추가하거나 추가적인 기능을 더하기 위해 프로토콜을 확장(extend)하는 것이 가능하다.
## 프로토콜 문법
```swift
protocol SomeProtocol {
   // protocol definition goes here
}
```
- 프로토콜의 문법은 기존 클래스, 구조체, 열거형과 비슷하다.
## Property 요구사항
```swift
protocol SomeProtocol {
   var mustBeSettable: Int { get set }
   var doesNotNeedToBeSettable: Int { get }
}
```
- 프로토콜에서는 프로퍼티의 이름과 타입 그리고 gettable, settable을 명시한다.
- 필수 프로퍼티는 항상 var로 선언해야 한다.
```swift
protocol AnotherProtocol {
	static var someTypeProperty: Int { get set }
}
```
- 타입 프로퍼티는 static 키워드를 적어 선언한다.
## Method 요구사항
```swift
protocol SomeProtocol {
	static func someTypeMethod()
}
```
- 필수 메서드 지정시 함수명과 반환값을 지정할 수 있고, 구현에 사용하는 괄호는 적지 않아도 된다.
## 프로토콜 초기 구현(Protocol Default Implementation)
- extension으로 protocol에 정의된 것들을 미리 구현함으로서 해당 protocol을 구현하는 대상들이 코드의 중복을 피할 수 있게 해줌
```swift
// 프로토콜 정의
protocol Person {
	var name: String? { get }
	var age: Int? { get }

	func getName() -> String?
	func getAge() -> Int?
}

// 프로토콜 기능 확장
extension Person {
	func getName() -> String? {
		return self.name
	}

	func getAge() -> Int? {
		return self.age
	}
}
```
- 위 설명대로 protocol에는 선언부(정의)만 표기하고 해당 기능을 확장(extension)하여 주었다.
```swift
struct Student: Person {
	var name: String?
	var age: Int?

	init(name: String?, age: Int?) {
		self.name = name
		self.age = age
	}
}
```
- 이어서 Student 구조체가 Person 프로토콜을 채택(준수)한다.
```swift
let channy = Student(name: "channy", age: 28)
print(channy.getName()) // channy
```
- Student 구조체를 초기화하고, .(dot) 문법을 통해 getName 메소드를 호출하면 이름이 출력됩니다.

# [[Generic]]의 활용
```swift
// 프로토콜 정의
protocol Stackable {
	associatedtype item
	var items: [Item] { get set }

	mutating func push(with item: item)
	mutating func pop() -> Item?
}

// 프로토콜 기능 확장
extension Stackable {
	mutating func push(with item: item) {
		items.append(item)
	}

	mutating func pop() -> item? {
		return items.popLast()
	}
}

// Stackable 프로토콜을 준수하는 제네릭 타입 구조체 정의
struct Stack<T>: Stackable {
	var items: [T]
	typealias item = T
}

var myStack = Stack<Int>(items: [1, 2, 3, 4])
myStack.push(with: 5)
print(myStack.pop()) // 5
```
- 스위프트에는 [[Stack]]이나 [[Queue]]의 자료구조가 없기 때문에 직접 구현해서 사용해야한다.
	- associatedtype은 해당 프로토콜을 채택하는 데이터 타입이 제네릭일 때 사용한다.
	- mutating 키워드를 사용해 인스턴스에서 변경 가능하다는 것을 표시할 수 있다.
	- 이 mutating 키워드는 값 타입 형에만 사용한다.