# TableView
- [[TableView]]의 각 row의 UI나 작업을 처리하는 부분
## 비동기 작업 처리
- TableViewCell 에서 이미지를 표시하는 일을 구현할 때 오래걸리는 작업을 전달하면 안된다. 
	- 비동기적인 작업이 일어날 수 있는 오래걸리는 일을 전달해주면 안된다.
- **이미지 url만 전달하고 cell에서 직접적으로 image를 로드하는 코드를 작성하자.**
- **빠르게 스크롤하는 경우를 대비해서 이미지를 받아온 데이터의 url하고 cell이 원래 가지고 있던 url하고 비교하는 코드도 작성해줘야한다.**
- 이 부분은 [[CollectionViewCell]]에서도 마찬가지 이다.

## prepareForReuse
- cell이 재사용되기 전에 호출되는 메서드
- super.prepareForReuse()를 호출해줘야한다.
- cell이 재사용될때 기존에 있는 imageView에 nil 처리를 해주지 않으면 cell이 재사용될때 이전에 사용한 이미지를 가지고 있을수도 있기 때문에 이미지가 변경되는 것 같은 현상을 볼수있다.
- 이 부분도 [[CollectionViewCell]]에서도 적용된다.