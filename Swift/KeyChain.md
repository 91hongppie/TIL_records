- Swift에서 민감 정보를 저장할 때 사용!
# UserDefaults
- UserDefaults에도 데이터를 수비게 저장할 수 있지만, 단순히 .info 파일에 키-값 쌍을 텍스트 형태로 저장하기 때문에 OS를 탈옥하면 내용물을 볼 수 있다는 문제가 있다.
- 보안이 필요한 데이터에는 적합하지 않다.
# KeyChain
- 이를 방지하기 위해 암호나 API Token과 같은 민감한 정보는 KeyChain에 저장하는 것이 좋다.
## 무엇을 저장할까?
- 로그인 및 암호 (해시)
- 결제 데이터
- 알고리즘 암호화를 위한 키
- 등등... 단순한 구조의 비밀을 유지하고 싶은 것들을 저장
## KeyChain 특징
- 사용자가 직접 제거하지 않는 이상, 앱을 제거하고 설치해도 데이터는 남아있다.
- 디바이스를 Lock하면 KeyChain도 잠기고, 디바이스를 Unlock하면 KeyChain도 풀린다.
	- KeyChain이 잠긴 상태에서는 Item들에 접근할수도, 복호화 할수도 없다.
	- KeyChain이 풀린 상태에서도 해당 Item을 생성하고 저장한 어플리케이션에서만 접근이 가능하다.
- 같은 개발자가 개발한 여러 앱에서 KeyChain 정보를 공유할 수 있다.

## KeyChain Service API
- KeyChain Service API로 민감한 데이터를 암호화 / 복호화하며 재사용하는 행위를 보다 쉽고 안전하게 사용할 수 있게한다.
## KeyChain Items
- 키체인에 저장된 Data 단위. 키체인은 하나 이상의 KeyChain Item을 가질 수 있다.

## KeyChain Item Class
- 저장할 Data의 종류
	- kSecClassInternetPassword
	- kSecClassCertificate
	- kSecClassGenericPassword
	- kSecClassIdentity
	- kSecClassKey
- 대표적으로 인터넷용 아이디/패스워드를 저장할 때 사용하는 kSecClassInternetPassword
- 인증서를 저장할 때 사용하는 kSecClassCertificate
- 일반 비밀번호를 저장할 때 사용하는 kSecClassGenericPassword 등이 있다.

## Attributes
- KeyChain item을 설명하는 특성, item class에 따라 설정할 수 있는 attributes가 달라진다.
- 애플 문서를 보면 각 아이템 클래스별로 다양한 어트리뷰트가 존재한다.

## 구현해보기
- Token 구조체 배열을 KeyChain으로 저장하자.
- 일반 비밀번호를 저장할 때 사용하는 kSecClassGenericPassword 라는 KeyChain Item Class를 사용하여 TOTP토큰배열을  저장하는 과정에 대해 살펴보도록 하자.
### KeyChain Query 작성하기
```swift
-------------------------------------------------
kSecClass: 키체인 아이템 클래스 타입,
kSecAttrService: 서비스 아이디, // 앱 번들 아이디
kSecAttrAccount: 저장할 아이템의 계정 이름
kSecAttrGeneric: 저장할 아이템의 데이터
-------------------------------------------------

private let account = "TokenService"
private let service = Bundle.main.bundleIdentifier

let query: [CFString: Any] = [
							  kSecClass: kSecClassGenericPassword, 
							  kSecAttrService: service, 
							  kSecAttrAccount: account, 
							  kSecAttrGeneric: data
							  ]
```
### API 메서드
#### Create
- SecItemAdd(\_:\_:)
- 키체인에 하나 이상의 항목을 추가할 때 사용
```swift
func createTokens(_ token: [Token]) -> Bool {
	guard let datat = try? JSONEncoder().encode(token),
		let service = self.service else { return false }

	let query: [CFString: Any] = [
		kSecClass: kSecClassGenericPassword, 
		kSecAttrService: service, 
		kSecAttrAccount: account, 
		kSecAttrGeneric: data
	]
	return SecItemAdd(query as CFDictionary, nil) == errSecSuccess
}
```
#### Read
- SecItemCopyMatching(\_:\_:)
- 검색 쿼리와 일치하는 키체인 항목을 하나 이상 반환하는 기능.
- 또한, 특정 키 체인 항목의 속성을 복사할 수 있다.
```swift
func readTokens() -> [Token]? {
	guard let service = self.service else { return nil }
	let query: [CFString: Any] = [
		kSecClass: kSecClassGenericPassword, 
		kSecAttrService: service, 
		kSecAttrAccount: account, 
		kSecAttrGeneric: data
	]
	
	var item CFTypeRef?
	if SecItemCopyMatching(query as CFDictionary, &item) != errSecSuccess {
		return nil 
	}

	guard let existingItem = item as? [String: Any],
		let data = existingItem[kSecAttrGeneric as String] as? Data
		let tokens = try? JSONDecoder().decode([TOTPToken].self, from: data) else { return nil }

	return tokens
}
```
#### Update
- SecItemUpdate(\_:\_:)
- 검색 쿼리와 일치하는 항목을 수정할 수 있는 기능
```swift
func updateTokens(_ token: [Token]) -> Bool {
	guard let query = self.query,
		let data = try? JSONEncoder().encode(token) else { return false }

	let attributes: [CFString: Any] = [
		kSecAttrAccount: account,
		kSecAttrGeneric: data
	]

	return SecItemUpdate(query as CFDictionary, attributes as CFDictionary) == errSecSuccess
}
```
#### Delete
- SecItemDelete(\_:)
- 검색 쿼리와 일치하는 항목을 제거하는 기능
```swift
func deleteTokens() -> Bool {
	guard let query = self.query else { return false }
	return SecItemDelete(query as CFDictionary) == errSecSucces
}
```