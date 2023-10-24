
- iOS13 이상에서 사용 가능
- 시스템 bar의 기본 모양을 커스텀 하기위한 객체
- navigationBar, tabBar, toolBar가 공유하는 공통 trait 프로퍼티들을 포함하고 있다.  
![](https://blog.kakaocdn.net/dn/ozFWQ/btqzPnBARFi/NHFBdVQFy7Y9bANzPVaWG1/img.png)
- 특정 타입의 bar를 구성할 때 일반적으로 적절한 Bar Appearance 하위 클래스를 인스턴스화 할 수도 있지만, UIBarAppearance 객체를 생성하고 프로퍼티들을 구성한 다음, 이를 사용하여 앱에서 새로운 BarAppearance 객체를 생성 할 수도 있다.
- UIBarAppearance 객체를 직접 만들어도 된다고 한다.
- navigationBar, TabBar, ToolBar가 공유하는 공톨 trait 프로퍼티들을 포함하고 있다고 했으니
![](https://blog.kakaocdn.net/dn/bbcoCU/btqzPmbB2mY/j59ZItRy0NhaC8JVUNeFU1/img.png)
- 위 3개의 Appearance 클래스가 UIBarAppearance를 상속받고 있겠다.