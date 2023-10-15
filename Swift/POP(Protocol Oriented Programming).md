# POP 탄생 배경
- 일반적으로 OOP에서 클래스의 상속 개념을 통해 공통 기능들을 모듈화하여 사용할 수 있었으나, 구조체 혹은 열거형의 경우에는 상속이 불가하기에 같은 타입에 대해서 공통적인 기능 구현을 위해서는 다른 방법을 이용해야 한다.
- 이를 해결하기 위한 방법이 Apple WWDC15(Swift 2)에서 [[Extension]]이 발표되었다
- [[Protocol]](청사진)을 구현하고 [[Extension]]으로 해당 프로토콜의 기능을 확장하는 형태로 사용한다.
- 이를 프로토콜 초기 구현 (Protocol Default Implementation)이라고 표현한다.
# POP의 장점
- 코드의 중복을 최소화 할 수 있다.
- 가볍고 안전하다
	- 상속과 달리 필요한 것만 골라서 쓸 수 있다.
	- 상속의 경우, 참조 타입이므로 참조 추적을 위한 비용이 많이 발생하기 때문에 속도 측면에서 다소 느리다.
- 값 타입의 상속 효과
	- 공통된 기능을 쉽게 구현할 수 있다.
- 수평적인 확장 기능
	- [[Class]]는 하나의 상속만 가능하고 수직적인 구조가 나타나지만 [[Protocol]]을 이용하면 수평적인 확장이 가능하다.
- 제네릭의 활용
	- 예를들어, Swift의 Array의 경우 데이터 타입의 관계없이 만들수 있고 이들 모두가 그에 따른 메서드를 사용할 수 있다.
# [[Protocol]]
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
	- [[Associated Type]]은 해당 프로토콜을 채택하는 데이터 타입이 제네릭일 때 사용한다.
	- mutating 키워드를 사용해 인스턴스에서 변경 가능하다는 것을 표시할 수 있다.
	- 이 mutating 키워드는 값 타입 형에만 사용한다.

