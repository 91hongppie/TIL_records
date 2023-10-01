- 구조체에서 init 함수가 없을때 자동으로 제공되는 init 함수


- 구조체건 클래스건 인스턴스 생성자 호출이 끝나는 시점에는 모든 프로퍼티가 초기화 되어 있어야 한다.
- 프로퍼티는 기본값을 지니지 않을 경우 무조건 생성자에서 초기화 해야한다.
- 다만 구조체는 init 함수가 없어도 에러가 나지 않는다.
- 클래스와 달리 구조체는 **따로 생성자를 구현하지 않았을 때** 모든 프로퍼티를 초기화 할 수 있게하는 Memberwise라는 생성자를 자동으로 제공한다.
```swift
struct PointStruct {
	let x: Int
	let y: Int
}
```
- 위처럼 PointStruct는 생성자를 따로 구현하지 않았기 때문에 자동으로 Memberwise Initializer가 제공된다.
![](https://blog.kakaocdn.net/dn/qeaWP/btqZP1ZGsn1/F4dYrxwQD0TSBGlXf2uLlK/img.png)
- 만약 생성자를 "직접" 구현 한다면
```swift
struct PointStruct {
	let x: Int
	let y: Int

	inti(value: Int) {
		self.x = value
		self.y = value	
	}
}
```
![](https://blog.kakaocdn.net/dn/5XWYY/btqZP2RRJVI/04DpYuJteJiH1KAm7NpM7K/img.png)
- Memberwise Initializer는 더 이상 제공되지 않는다.
- 하지만 [[Extension]]을 사용하면 Memberwise Initializer를 보존하면서 새로운 생성자를 추가할 수 있다.
```swift
struct PointStruct {
	let x: Int
	let y: Int
}

extension PointStruct {
   init(value: Int) {
	   self.x = value
	   self.y = value
   }
}
```
- [[Extension]]을 통해 (구조체 한정) 생성자를 추가하면
![](https://blog.kakaocdn.net/dn/bPkNye/btqZMmXQrqw/2iH6IuTjGjS7U9ZfG4q2r0/img.png)
- Memberwise Initializer를 보존하며 생성자를 추가할 수 있다.