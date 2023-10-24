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

## .standardAppearance
- largeTitle이 없는 size의 navigationBar의 모습 세팅
## .compactAppearance
- compact-height navigation bar의 모습 세팅
- 작은 iPhone에서 landscape일 때 모습이라고 한다.

## .scrollEdgeAppearance
- scrollable한 content의 edge가 NavigationBar에 일치하는 edge에 도달할 때의 모습 세팅
- 
