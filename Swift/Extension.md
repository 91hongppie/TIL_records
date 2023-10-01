- [[Class]], [[Struct]], [[Enum]] 타입에 새로운 메서드, 프로퍼티, 생성자를 추가적으로 정의해 사용하기 위해 사용된다.
- 이때 저장 프로퍼티는 extension에 정의할 수 없고, 연산 프로퍼티만 정의할 수 있다.
- 소멸자는 추가할 수 없고 생성자는 convenience init만 정의할 수 있다.
- struct의 경우에는 기존 struct에서는 생성자를 직접 구현하면 memberwise initializer(기본 생성자)가 사라지지만 구조체의 Extension에 생성자를 정의하면 memberwise initializer가 사라지지 않는다.
- where를 사용하면 특정한 조건을 가진 타입에 대해서만 Extension을 적용할 수 있다.
```swift
extension Array where Element: Idable {
	func filterWithId(id: String) -> [Element] {
		return self.filter { (item) -> Boold in
			return item.id == id
		}
	}
}
```