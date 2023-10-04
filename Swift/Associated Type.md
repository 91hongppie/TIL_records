# Associated Type
- 프로토콜을 정의할 때, 몇몇을 associated type으로 선언하면 매우 유용할 때가 있다.
- Associated Type은 프로토콜의 일부로 사용되는 타입을 위한 placeholder 역할을 한다.
- Associated Type은 정의하는 프로토콜이 채택되기 전까지 실제 타입이 명시되지 않는다.
- Associated Type은 associatedtype 키워드를 사용해서 정의한다.
# Associated Types in Action
- Container 프로토콜이 associated type의 Item과 함께 정의되어 있다.
```swift
Protocol Container {
	associatedtype Item
	mutating func append(_ item: Item)
	var count: Int { get }
	subscript(i: Int) -> Item { get }
}
```
- 이 프로토콜은 3가지의 요구사항을 정의한다.
	1. append(_:)
		- 메서드를 통해서 컨테이너에 새로운 항목을 추가할 수 있어야한다.
	2. count
		- Int 타입
		- 컨테이너에 들어있는 항목의 갯수를 알 수 있어야한다.
	3. subscript
		- Int 타입
		- 컨테이너의 각각의 항목을 가져올 수 있어야한다.
- Container 프로토콜은 항목들이 컨테이너에 어떻게 저장되어야 하는지, 어떤 타입이어야 하는지는 정의하고 있지 않고, 3가지 필수 요구사항만 정의한다.
- 이 프로토콜을 준수하는 타입은 세가지 필수 요구사항만 준수하면 원하는 기능을 더할 수 있다.
- Container 프로토콜을 준수하는 모든 타입은, 저장하는 값의 타입을 명시해야 하고, 이 값은 컨테이너에 추가될 수 있는 타입임을 보장해야한다.
- 