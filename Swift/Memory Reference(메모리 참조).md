# ARC(Automatic Reference Counting)
- 컴파일 시 코드를 분석해서 자동으로 retain, release 코드를 생성해주는 것
- 참조된 횟수를 추적해 더 이상 참조되지 않는 인스턴스를 메모리에서 해제해 주는 것

- ARC는 자동으로 RC를 관리해주기 때문에 메모리 해제에 대한 개발자의 부담을 덜어준다.


# Strong(강한 참조)
- 해당 인스턴스의 소유권을 가진다.
- 자신이 참조하는 인스턴스의 retain count를 증가시킨다.
- 값 지정 시점에 retain이 되고 참조가 종료되는 시점에 release가 된다.
- 선언할 때 아무것도 적어주지 않으면 default로 strong이 된다.
```swift
var test = Test() // retain count 1 증가
test = nil // retain count가 1 감소되어 0이 되면서 메모리 해제됨
```

# Weak(약한 참조)
- 해당 인스턴스의 소유권을 가지지 않고, 주소값만을 가지고 있는 포인터 개념이다.
- 자신이 참조하는 인스턴스의 retain count를 증가시키지 않는다. release도 발생할 일이 없다.
- 자신이 참조는 하지만 weak 메모리를 해제시킬 수 있는 권한은 다른 클래스에 있다.
- 메모리가 해제될 경우 자동으로 레퍼런스가 nil로 초기화 해준다.
- weak 속성을 사용하는 객체는 항상 optional 타입이어야 한다. (해당 객체가 nil일 수 있기 때문에)
```swift
// 객체가 생성되지만 weak이기 때문에 바로 객체가 해제되어 nil이 된다.
weak var test = Test()
```

# unowned (미소유 참조/약한 참조)
- 해당 인스턴스의 소유권을 가지지 않는다.
- 자신이 참조하는 인스턴스의 retain count를 증가시키지 않는다.
- nil이 될 수 없다. optional로 선언 되어서는 안된다.
```swift
// 객체 생성과 동시에 해제되고 댕글링 포인트만 가지고 있음. 에러남.
unowned var test = Test()
```
## Weak와 unowned의 차이
- weak는 객체를 계속 추적하면서 객체가 사라지게 되면 nil로 바꾼다.
- 하지만, unowned는 객체가 사라지게 되면 댕글링 포인터가 남는다.
- 이 댕글링 포인터를 참조하게 되면 crash가 나는데, 이 때문에 unowned는 사라지지 않을거라고 보장되는 객체에만 설정하여야 한다.
