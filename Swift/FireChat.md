![[Simulator Screenshot - iPhone 15 Pro Max - 2023-10-24 at 18.28.00 1.png]]

```swift
func configureUI() {
	view.backgroundColor = .white

	configureNavigationBar()

	let image = UIImage(systemName: "person.circle.fill")
	navigationItem.leftBarButtonItem = UIBarButtonItem(image: image, style: .plain, target: self, action: #selector(showProfile))
}

func configureNavigationBar() {
	let appearance = UINavigationBarAppearance()
	appearance.configureWithOpaqueBackground()
	appearance.largeTitleTextAttributes = [.foregroundColor: UIColor.white]
	appearance.backgroundColor = .systemPurple
	navigationController?.navigationBar.standardAppearance = appearance
	navigationController?.navigationBar.compactAppearance = appearance
	navigationController?.navigationBar.scrollEdgeAppearance = appearance
	navigationController?.navigationBar.prefersLargeTitles = true
	navigationItem.title = "Messages"
	navigationController?.navigationBar.tintColor = .white
	navigationController?.navigationBar.isTranslucent = true
	navigationController?.navigationBar.overrideUserInterfaceStyle = .dark
}
```

## UINavigationBarAppearance
- iOS 13 이상에서 사용할 수 있다.
- [[UIBarAppearance]]를 상속받는다.
- NavigationBar의 색상이나 디자인을 변경하거나 할 때 사용한다.

## .configureWith______
- 그림자 값을 생성한다.
## .configureWithOpaqueBackground
- 불투명한 색상의 백그라운드 생성
## .configureWithDefaultBackground
- 반투명한 그림자를 백그라운드 앞에 생성
## .configureWithTransparentBackground
- 그림자 제거하고 기존의 백그라운드 색상을 사용

## .largeTitleTextAttributes
- largeText에 대한 style을 지정한다.

## .backgroundColor
- navigationBar에 대한 배경색 지정



# navigationController
## .standardAppearance
- largeTitle이 없는 size의 navigationBar의 모습 세팅
## .compactAppearance
- compact-height navigation bar의 모습 세팅
- 작은 iPhone에서 landscape일 때 모습이라고 한다.
## .scrollEdgeAppearance
- scrollable한 content의 edge가 NavigationBar에 일치하는 edge에 도달할 때의 모습 세팅
- 스크롤된 content의 edge가 해당 bar에 도달하면, UIKit이 이 프로퍼티의 appearance settings를 적용한다고 한다.
## .prefersLargeTitles
- true
	- 큰 타이틀을 사용하겠다는 뜻
- false
	- 큰 타이틀을 사용하지 않겠다는 뜻
	- 
## .tintColor
- navigationBar의 아이콘이나 글자 색상
## .isTranslucent
- 반투명인지 여부를 세팅한다.
## .overrideUserInterfaceStyle
- 해당 부분에서만 테마 덮어쓰기

# navigationItem
## .title
- navigationBar의 title
