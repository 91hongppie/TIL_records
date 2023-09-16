- 네트워크 작업같은 여러 페이지에서 사용하는 Model은 싱글톤 패턴을 사용하자.
	- NetworkManager를 또 생성하지 못하게 init에 private을 붙여 외부에서 또 생성하지 못하게 한다.
```swift
class NetworkManager {
	static let shared = NetworkManager()

	private init() {}

	...
}
```