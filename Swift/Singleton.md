- 네트워크 작업같은 여러 페이지에서 사용하는 Model은 싱글톤 패턴을 사용하자.
	- NetworkManager를 또 생성하지 못하게 init에 private을 붙여 외부에서 또 생성하지 못하게 한다.
```swift
class NetworkManager {
	static let shared = NetworkManager()

	private init() {}

	...
}
```


# Singleton 패턴이란
- 애플리케이션이 시작될 때 객체의 인스턴스를 최초 1회만 생성(static)하여 사용하는 디자인 패턴
# Singleton 클래스 생성 방법
```swift
class SingletomClass {
	static let shared = SingletonClass()

	private init() {}
}
```
- 스위프트에서는 static let으로 객체의 인스턴스를 할당해주면 끝!
- 인스턴스가 추가로 생성되는 것을 방지하기위해 init() 함수의 접근 제어자를 private으로 선언한다.
# Singleton 사용 예제
```swift
class AppInfo {
	static let shared = AppInfo()

	private init() {}

	var mainInfo: [String: Any]? {
		guard let info = Bundle.main.infoDictionary else { return nil }

		return info
	}

	var name: String? {
		self.mainInfo?["CFBundleName"] as? String
	}

	var scheme: String? {
		guard let urlTypes = self.mainInfo?["CfBundleURLTypes"] as? [AnyObject],
			let urlTypeDictionary = urlTypes.first as? [String: AnyObject],
			let urlSchemes = urlTypeDictionary["CFBundleURLSchemes"] as? [AnyObject]
			let scheme = urlSchemes.first as? String else { return nil }

		return scheme
	}

	var version: String? {
		self.mainInfo?["CFBundleShortVersionString"] as? String
	}
}
```
- 앱 정보의 프로퍼티를 저장하고 있는 AppInfo 클래스를 싱글톤으로 작성한 코드
```swift
let appInfo = AppInfo.shared

if let appName = appInfo.name,
	let appScheme = appInfo.scheme,
	let appVersion = appInfo.version {
		print("appName: \(appName)")
		print("appScheme: \(appScheme)")
		print("appVersion: \(appVersion)")
	}
```
- appInfo 변수에 AppInfo 클래스의 shared(인스턴스)를 가져온다.
- 이제 어떤 화면(클래스)에서든 해당 클래스의 프로퍼티에 접근할 수 있다.
# Singleton 패턴의 장단점
## 장점
- 인스턴스를 최초 1회만 생성하므로 메모리와 성능 측면에서 효율이 좋다.
- 클래스 간 데이터 공유가 쉽다.
- 인스턴스가 1개라는 것을 보증받는다. (Thread Safe)
## 단점
- 싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우 다른 클래스의 인스턴스들 간에 결합도가 높아져 개방-폐쇄 원칙(OCP, Open-Closed Principle)을 위배하게 된다.
	- 따라서 수정과 테스트가 어려워진다.
- 싱글톤을 위한 코드를 구현해야함
	- 일반적으로는 그렇지만 스위프트에서는 매우 간단하게 구현할 수 있다.
# Thread Safe
- 여러 스레드에서 어떤 객체에 대해 동시에 접근이 이루어져도 프로그램의 동작에 이상이 없는 것을 뜻한다.
	- 예를 들어 멀티 스레드 환경에서 동시에 싱글톤을 사용하는 경우 인스턴스가 2개 이상 생성되는 경우가 생길 수 있다. 이 경우에 Thread Safe가 보장되지 않는다.

```swift
# import "AppInfo.h"

@implementation AppInfo

+ (instancetype)getInstance {
	static AppInfo *_instance = nil;
	static dispatch_once_t oncePredicate;
	dispatch_once(&oncePredicate, ^{
		_instance = [[AppInfo alloc] init];
	});
	return _instance;
}

@end
```
- 이를 방지하고자 Objective-C에서는 dispatch_once_t를 사용하여 인스턴스가 1회만 생성된다는 것을 보장했었다.
- 스위프트에서는 이런 코드가 없는데 스위프트에서는 static let으로 선언하는 것만으로도 1회 생성을 보장받기 때문이다.