---
title: "[Swift] Table View 만들기"
excerpt: "table view, table view cell, delegate 를 정리해보자."
date: 2021-03-04 21:24:00 -0400
category: Syntax
---

> CATEGORY `Syntax`
> 스위프트 문법을 정리합니다.

오늘은 테이블뷰 를 만드는 방법에 대해 정리할 예정인데요. 테이블뷰를 만드는 법을 다루기 전에 먼저 테이블 뷰가 무엇인지에 대해 간단히 살펴보도록 하겠습니다.

<br>

# 🤔 테이블 뷰가 뭔데?
테이블 뷰는 다양한 앱에서 (거의) 필수적으로 사용되고, 쉽게 볼 수 있는 화면인데요. 아이폰의 메시지, 아이폰의 메모, 카카오톡, 인스타그램 등 매우 많은 앱에서 볼 수 있습니다.

바로 이런 화면이 테이블 뷰를 사용한 화면들 입니다.

![](https://user-images.githubusercontent.com/77034159/109977141-dbdc6d80-7d3f-11eb-8dcc-7d397ee658c6.JPEG)

위 화면처럼 비슷한 셀들이 아래로 주르륵 나열되어 있는 화면이 테이블 뷰 입니다. 즉, 메모장이나, 채팅, 장바구니 화면 등 다양한 기능을 구현하기 위해선 필수적인 뷰 입니다!

<br>

# 🔨 테이블 뷰, 어떻게 만들지?

## 1. 스토리보드에서 Table View, Table View Cell 을 추가하자

![](https://user-images.githubusercontent.com/77034159/109910537-ae65d480-7ceb-11eb-9000-65f9152823f3.gif)

1. 스토리보드의 `+`  버튼을 누릅니다.

2. `table` 을 검색합니다.
3. `Table View` 를 드래그해서 화면에 추가합니다.
4. `Table View Cell` 을 드래그하여 `Table View` 내부에 추가합니다.

<br>
<br>

## 2. DataSource 와 Delegate 를 View Controller 로 설정하기

![](https://user-images.githubusercontent.com/77034159/109911652-cd656600-7ced-11eb-84ec-94a3c47e7b3a.gif)

1. `Table view` 를 클릭 후, `View Controller` 에 `ctrl + drag` 합니다. (파란색 화살표가 나옵니다.)

2. `DataSource` 와 `Delegate` 를 선택합니다.
3. 끝!

`Table View` 의 `dataSource` 와 `delegate` 를 `View Controller` 로 설정합니다. 즉, 테이블 뷰의 외형 (row 개수, row 높이 등등)과 눌렀을 때 어떻게 동작할지 등을 뷰 컨트롤러가 담당하는 것 입니다.

<br>
<br>

## 3. Table View Cell 의 내부를 Custom 하자

![](https://user-images.githubusercontent.com/77034159/109913326-1cf96100-7cf1-11eb-9947-84fe768a1669.gif)

![](https://user-images.githubusercontent.com/77034159/109915272-ddcd0f00-7cf4-11eb-8a4a-088609bac88a.gif)

1. 스토리보드에서 `Label` 을 추가합니다. (또는 `Image View` 를 넣어도 상관 없습니다.)
2. Custom 클래스를 하나 만듭니다. 이 때, `UITableViewCell` 을 상속 받도록 합니다.
	```swift
	class CustomCell: UITableViewCell {
		@IBOutlet weak var labelTitle: UILabel!
		@IBOutlet weak var labelContent: UILabel!
	}
	```

3. 스토리보드의 `Inspectors` 에서 `Identity inspector` 로 들어가보면, 해당 `Table View` 의 클래스를 설정할 수 있는데요. 이를 위에 만들었던 클래스인 `CustomCell` 로 설정합니다.
4. `ctrl + drag` 로 outlet 을 연결해줍니다.
5. 마지막으로 `Table View Cell` 의 `Identifier` 를 cell 로 설정해 줍니다. (나중에 필요해요)
	![](https://user-images.githubusercontent.com/77034159/109917660-0bb45280-7cf9-11eb-9ba1-8ee90df57c54.png")

<br>
<br>


## 4. Table View Cell 의 data 를 만들자 

1. `Table View` 에 표시될 title 과 content 를 배열로 만들어 봅시다. (코드 위치는 `View Controller` 내부)
	```swift
	let memoTitle = ["오늘 먹은 음식", "커피", "맛집 추천", "오늘 할 일", "과제", "스터디 날짜"]
	let memoContent = ["등촌칼국수, 너무 맛있다!!", "오늘은 커피를 안 마셨다.", "마늘 닭볶음탕 먹어보고 싶다. 궁금해", "오늘 테이블 뷰 블로그에 업로드하기 목표", "휴학해서 과제 없다. 부럽지", "매주 월요일 오후 4시에 시작합니다."]
	```
	
2. 끝!


<br>
<br>

## 5. Protocol 을 채택하고 필수 메서드를 작성하자
1. ViewController 에 UITableViewDataSource 와 UITableViewDelegate 프로토콜을 채택합니다.
	```swift
	class ViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
		// code...
	}
	```
	<br>
	
2. 이러면 바로 오류가 뜨는데요. 그 오류를 클릭하여 `fix` 버튼을 누르면 아래와 같은 필수 메서드가 저절로 생성이 됩니다. 
	```swift
	func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
		// code
	}

	func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
		// code
	}
	```
	* 그 외의 메서드를 추가하고 싶다면? 


	* `Jump to Definition` 을 클릭하여 다양한 메서드들이 뜨니까 원하는 메서드를 사용하면 됩니다.

<br>

3. 이제 위 메서드의 내부 코드만 작성하면 됩니다.
	1. row 의 개수 설정하기
	```swift
	func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
		return memoTitle.count		// 배열 크기를 반환
	}
	```
	<br>
	
	2. 각 row 에 나타낼 cell 설정하기
	```swift
	func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
		guard let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as? CustomCell else {
			return UITableViewCell()	
		}
		cell.labelTitle.text = memoTitle[indexPath.row]
		cell.labelContent.text = memoContent[indexPath.row]
		return cell
	}
	```
	* `cell` 을 `CustomCell` 로 캐스팅하여, 존재하는 경우는 `cell` 을 반환, 존재하지 않는 경우에는 `UITableViewCell()` 을 반환합니다.
	* 여기서 `withIdentifier` 값을 이전에 설정해둔 `Table View Cell` 의 Identifier 와 동일하게 설정해야 합니다.
	<br>

	3. (선택) 높이를 지정하기 

	```swift
	func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
		return 100.0
	}
	```

<br>
<br>

## 6. 조금 더 꾸며보자

![](https://user-images.githubusercontent.com/77034159/109920083-1d97f480-7cfd-11eb-95ca-f327f308e24e.gif)

이 화면은 아무것도 꾸미지 않은 화면입니다. 글씨 크기와 굵기는 스토리보드에서 설정해주었습니다.

<br>

![](https://user-images.githubusercontent.com/77034159/109921253-e9bdce80-7cfe-11eb-831b-28fba918d1fd.gif)

이 화면은 다음과 같이 조금 꾸민 화면 입니다.

<br>

### 배경 색 설정하기
1. `ViewController` 내부에 있는 `viewDidLoad()` 부분에 코드를 다음과 같이 작성합니다.
	```swift
	self.view.backgroundColor = .systemGray6	// 색상 이름
	```
	
2. 위처럼 색상명을 이용해도 되고, `Color Literal` 로 원하는 색상을 선택해도 됩니다.

<br>

### Table View 코너 둥글게 설정

1. `ViewController` 내부에 있는 `viewDidLoad()` 부분에 코드를 다음과 같이 작성합니다.
	```swift
	self.tableView.layer.cornerRadius = 12.0	// 반지름
	```
	
2. 끝!

<br>

### Label 추가
제목과 총 메모의 개수를 나타내는 `Label` 을 추가하였습니다.

1. 스토리보드에서 `Label` 을 추가합니다.

2. 제목은 스토리보드에서 `text` 속성을 설정해 줍니다.
3. 메모의 개수를 나타내는 `Label` 은 아웃렛변수로 선언해 줍니다.
	```swift
	@IBOutlet weak var countLabel: UILabel!
	```
4.  `text` 속성은 `viewDidLoad()` 에 다음과 같이 설정합니다.
	```swift
	self.countLabel.text = "총 \(memoTitle.count) 개의 메모가 있습니다."
	```


<hr>

오늘은 테이블 뷰를 구현해보았는데요! 어려운 부분이 있다면 언제든 댓글 주세요 👀  감사합니다.
