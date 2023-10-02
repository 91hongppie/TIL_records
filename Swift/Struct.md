# 구조체 (Struct)
- 인스턴스의 값(프로퍼티)을 저장하거나 기능(메서드)을 제공하고 이를 캡슐화 할 수 있는 swift가 제공하는 타입(named type)이다.
- [[Class]]처럼 인스턴스를 만들어서 실제 작업에도 쓸 수 있다.
```swift
struct name {
	var name = "Song"

	func my_name() {
		print("my name is \(name)")
	}
}

var song: Name = Name()

print(song.name)
song.my_name()

song.name = "Kim"
song.my_name()
```
- [[Class]]에서 짰던 코드와 거의 비슷하다.
- class를 struct로 바꾼거 외에는 모두 동일하다.
- 이처럼 클래스와 구조체는 선언하고 사용하는 방법까지 매우 비슷하다.
- 클래스와 같이 구조체 안의 변수도 속성(프로퍼티)라고 부르고 함수도 메서드(Method)라고 부른다.
- 속성(Property)
	- 구조체 안의 변수
- 메서드(Method)
	- 구조체 안의 함수
- 인스턴스 선언
	- var song: Name = Name()
	- [[Class]]와 동일하다.
- 실행 결과
	- Song
	- my name is Song
	- my name is Kim
- 클래스와 다른 점
	- 클래스에서는 초기화 작업을 통해 인스턴스에 매개변수를 변경해줄 수 있었다. (클래스 내부에 init() 메서드 생성)
	- 구조체에서는 자동으로 초기화 코드를 만들어준다. - [[Memberwise initializer]]
```swift
struct Name {
	var name: String

	func my_name() {
		print("my name is \(name)")	
	}
}

var song: Name = Name(name: "Song")

print(song.name)
song.my_name()
```
- 위 코드에서 name속성의 값을 선언하지 않고 인스턴스 선언시 매개변수로 넣어준다.
- 클래스의 경우 init() 메서드가 필요하지만 구조체에서는 없어도 문제가 없다.
- 실행 결과
	- Song
	- my name is Song

# 구조체 초기화(Initialization)
- [[Class]]와 달리 Struct(구조체)는 **구조체 멤버를 파라미터 네임으로하여 스위프트가 자동으로 초기화 코드를 만들어준다.**([[Mem]])
- 직접 초기화 코드를 작성할 수도 있다.
- 하지만 초기화 코드를 직접 정의하면 자동 초기화 코드는 더 이상 제공받지 못한다.