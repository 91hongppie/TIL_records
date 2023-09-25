- 화면 이동을 ViewModel에서 하는 것을 기본적으로 추구한다.
- 실무에서는 ViewModel이 복잡해져서 실무에서는 Coordinator pattern을 사용한다.
	- Coordinator Pattern 화면 이동과 관련된 부분을 관리하는 객체를 따로 만든다.

# 왜 아키텍처 패턴이 필요할까?
## 왜 코드를 나누려고 하는가
- 한 곳에 코드를 모두 작성하면 협업하는데 방해가 된다.

# 의존성 주입(Dependency Injection)
- [[Protocol]]을 사용해서 의존성 분리 및 의존관계 역전시킴
- 주입을 하되 [[Protocol]] 타입으로 주입해서 여러가지 코드로 확장할 수 있도록한다.
## 주입의 개념
- 생성자를 통해서 저장 속성을 외부에서 주입한다.
```swift
class Person {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}

// 외부에서 값을 주입(할당/초기화)해서 인스턴스 생성
let p1 = Person(name: "뉴진스")
```

 