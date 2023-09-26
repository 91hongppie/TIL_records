- 각자의 역할과 책임을 나누는 것이 목적


- Model
	- 데이터 모델
	- 비즈니스 로직까지 포함
	- 뷰 컨트롤러가 모델을 소유하여 내부에 위치하게 된다.
- View
	- 화면 담당
	- storyboard로 만들면 따로 존재하지만 code로 작성하면 ViewController 내에 위치한다.
	- 코드로 UI 작성시에 일반적으로 View를 따로 분리하지 않고 (뷰 컨트롤러 내부에)작성하는 경우도 많음
- Controller
	- 관리 / 중재자

1. 사용자의 인풋이 ViewController에 전달된다.
2. 모델(데이터)을 변화시킴
3. ViewController에서 바뀐 결과를 받아옴
4. 받아온 결과를 가지고 다시 표시 시킴 (뷰를 다시 그림)

## 단점
- ViewController 코드가 너무 비대해진다.(모든 코드들이 ViewController에 들어가있다.)
- ViewController의 역할이 커진다.
- 테스트 코드 작성 불가능
- Code로 View를 작성할 경우 View랑 ViewController이 합쳐지는 경우가 많다.