- 일종의 자격증이라고 생각하자
- [[MVVM]]에서 의존성을 분리할 때 사용한다.
- 타입으로 사용 가능하다.

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
