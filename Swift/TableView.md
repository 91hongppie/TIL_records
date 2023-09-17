## TableViewDataSource
- required
	- numberOfRowsInSection()
	- cellForRowAt()
		- 이 함수에서 [[TableViewCell]]을 사용한다.
		- 각 row에 대한 처리를 해주는 함수로 tableView의 dequeueReusableCell에 사용할 cell을 할당해서 재사용되도록 한다.
## TableViewDelegate
- 필수 메서드가 없음
- optional
	- heightForRowAt
		- rowHeight를 직접적으로 구현하지 않고 Delegate heightForRowAt 메서드의 return 값을 통해 높이를 지정한다.
		- 직접적으로 높이를 지정하면 셀 높이를 row마다 다르게 설정이 불가능하다.
		- return 행의 높이
		- UITableView.automaticDimension
			- 이 값을 return하면 높이를 알아서 잡아준다.
	- estimatedHeightForRowAt
		- 추정된 높이
		- 유동적인 셀의 높이를 생각할 때는 여기다가 하는게 좋을것이다.

