- Swift에서는 클래스를 정의하여 객체를 만들고 사용할 수 있다.
- 클래스를 하나 만든다면 클래스에서 생성된 객체인 인스턴스를 만들어 실제 작업에 쓰일 수 있게한다.
- 코드를 통해 더 자세히 알아보자
```swift
class Name {
	var name = "Song"

	func my_name() {
		print("my name is \(name)")
	}
}

let song: Name = Name()

print(song.name)
song.my_name()

song.name = "Kim"
song.my_name()
```
- 클래스를 선언하기 위해서는 위 코드처럼 class 클래스이름 { 코드 } 이렇게 작성하면 된다.
- 클래스 안에 변수를 swift에서는 **속성**이라고 부르고 함수는 **메서드**라고 부른다.
	- 속성(Property)
		- 클래스 안의 변수
	- 메서드(Method)
		- 클래스 안의 함수
- 클래스를 사용할 수 있도록 **인스턴스**를 만들어준다.
	- **let song: Name = Name()**
- 클래스 내의 속성이나 메서드에 접근하기 위해서는 . 을 사용한다.
	- song.name
	- song.my_name()
- 위 코드의 실행 결과
	- Song
	- my name is Song
	- my name is Kim
# 클래스 상속
- 클래스 사용의 장점
	- 관계가 있는 함수나 변수를 한 곳에 모아 놓을 수 있다.
	- **프로그램의 재사용을 쉽게 할 수 있다.**
- 이런 재사용을 더 넣게 응용한 것이 바로 **상속**이라는 것이다.
- 상속은 기존의 클래스의 모든 기능을 이어 받아 새로운 클래스를 정의하는 것이다.
- 즉, 이미 편리한 클래스가 있으면, 그것을 상속받아 자신의 고유한 기능을 덧붙여서 자신만의 새로운 클래스를 쉽게 만들 수 있다.
```swift
class Name { // 슈퍼 클래스
	var name = "Song"

	func my_name() {
		print("my name is \(name)")
	}
}

class YourName: Name { // 클래스 상속!!
	var yourName = "Kim"

	func ourName() {
		print("my name is \(name) and your name is \(yourName)")
	}
}

let song: YourName = YourName()

print(song.name)  // "song" 출력
print(song.yourName) // "kim" 출력

song.my_name() // 클래스 상속으로 my_name() 메서드 사용 가능
song.ourName()
```
- 위의 클래스를 가져와서 YourName이라는 클래스에 상속을 시켰다.
- 이 때 가져온 Name 클래스를 **슈퍼클래스**라고 한다.
- 위 코드처럼 상속이 되었다면 이제 YourName 클래스 안에서 Name 클래스의 변수와 함수를 이용할 수 있다.
- YourName 클래스에는 name변수가 없지만 ourName 메서드에서 name 변수를 사용하는 것을 확인할 수 있다.
- 실행 결과
	- Song
	- Kim
	- my name is Song
	- my name is Song and your name is Kim

# 클래스 초기화 (Initialization)
- 위 코드에서 인스턴스를 생성할 때 인수없이 만들었다.
- 하지만 여러 인스턴스를 만들고 우리가 원하는 인수들까지 지정해줄 수 있다면 매우 편리해질 것이다.
- 이런 때에 이용되는 것이 "초기화(Initialize)" 이다.
- 이것은 인스턴스를 만들 때 자동으로 호출되는 초기화 처리 전용의 메서드이다.
```swift
class Name {
	var name: String
	var age: Int

	init(name: String, age: Int) {
		self.name = name
		self.age = age
	}

	func my_name() {
		print("my name is \(name) and \(age) year's old")
	}
}

let name1: Name = Name(name: "song", age: 24)
let name2: Name = Name(name: "kim", age: 25)

name1.my_name()
name2.my_name()
```
- 위 Name 클래스를 다시 한번 불러왔다.
- 클래스의 속성드에게 값을 지정해주지 않고 init() 메서드를 이용해서 초기화했다.
- init 메서드 안의 self는 자기 자신을 가리키는 값이다.
- 즉, self. 이 붙은 변수들은 클래스 내의 변수라는 것이다.
- name과 age 변수를 각각 지정해 준 뒤 인스턴스를 생성해보면 name: "song", age: 24 이렇게 인수들을 지정해 줄 수 있다.
- name1과 name2의 인수들을 다르게 지정한 후 my_name() 메서드를 실행 시켜보도록하자.
- 실행 결과
	- my name is song and 24 year's old
	- my name is kim and 25 year's old
- 인수를 다르게 지정해주어 두 인스턴스의 메서드들이 각각의 인수에 맞게 출력이 되는 것을 확인할 수 있다.