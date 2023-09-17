# CollectionView 주의사항
- UICollectionViewFlowLayout
	- 컬렉션 뷰의 레이아웃을 담당하는 객체
	- 컬렉션 뷰에 접근해서 collectionViewLayout에 할당해줘야 한다.
```swift
   // 컬렉션뷰 (테이블뷰와 유사)
    @IBOutlet weak var collectionView: UICollectionView!

    // 컬렉션뷰의 레이아웃을 담당하는 객체
    let flowLayout = UICollectionViewFlowLayout()
  

    func setupCollectionView() {
        // 컬렉션뷰의 레이아웃을 담당하는 객체
        //let flowLayout = UICollectionViewFlowLayout()
        collectionView.dataSource = self

        collectionView.backgroundColor = .white

        // 컬렉션뷰의 스크롤 방향 설정
        flowLayout.scrollDirection = .vertical

        let collectionCellWidth = (UIScreen.main.bounds.width - CVCell.spacingWitdh * (CVCell.cellColumns - 1)) / CVCell.cellColumns

        flowLayout.itemSize = CGSize(width: collectionCellWidth, height: collectionCellWidth)

        // 아이템 사이 간격 설정
        flowLayout.minimumInteritemSpacing = CVCell.spacingWitdh

        // 아이템 위아래 사이 간격 설정
        flowLayout.minimumLineSpacing = CVCell.spacingWitdh

        // 컬렉션뷰의 속성에 할당
        collectionView.collectionViewLayout = flowLayout

    }
```
