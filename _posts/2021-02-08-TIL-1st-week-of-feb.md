---
title: "📖 TIL: 1st Week of Feb"
excerpt: "2월 1주차에 내가 배운 것들을 정리해보자."
date: 2021-02-08 01:43:00 -0400
categories: TIL
---
> TIL: Today I Learned  
일주일 동안 공부한 내용을 정리

## MON - WED
알바와 과외 때문에 코딩할 시간이 없었다.

## THU
오랜만에 <u>swift</u>를 공부했다. 
1. 이전에 했던 간단한 `TableView` 프로젝트에 <u>MVVM 패턴</u>을 적용해보았다.
2. swift 문법을 공부할 겸 <u>프로그래머스 코딩테스트 연습문제</u>를 3개 정도 풀었다.

뭔가 코딩테스트를 하면서 코드 짧게 쓰는 법과 _오 이런 기능이 있었다니 ?!_ 를 배우고 있다.

## FRI
남자친구와 저녁을 먹으며 <u>iOS 개발 스터디</u>를 (우리끼리) 하기로 했다.  

각자 2월 목표를 정했다. 나는 <u>아이폰 계산기 클론 코딩</u>과 프로그래머스 <u>코딩테스트 1단계</u> 끝내기! 그래서 집 오자마자 아이폰 계산기와 최대한 비슷하게 디자인만 완성했다. 

원래는 항상 `@IBOutlet` 변수를 이용해서 `viewDidLoad()` 안에 속성값들을 바꿔줬는데 아이폰 계산기 버튼은 거의 비슷한 속성을 가지기 때문에 class를 통해 상속받아 쓸 수 있도록 코드를 작성했다.
그래서 위치 지정만 스토리보드를 이용하고 나머지 디자인은 코드로 작성했다. 뭔가 스토리보드로 디자인 한 것보다 더 뿌듯하다.

**📌 class를 통해 속성값들 상속받기**
```swift
// 1. UIButton 을 상속 받는 class 만들기
class ClassName: UIButton {
    required init(coder aDecoder: NSCoder){
        super.init(coder: aDecoder)!
        // 속성값들 지정
        self.layer.backgroundColor = UIColor.systemOrange.cgColor
        // ...
    }
}

// 2. storyboard 로 들어가서 버튼을 클릭 후, Custom class 를 ClassName 으로 변경해준다.
```

## SAT
코딩테스트 연습을 조금 하고, 아이폰 계산기 만들기에 집중했다. 

아이폰 계산기의 다음과 같은 기능을 구현했다.
1. 숫자 버튼으로 숫자 받아오기 
2. AC 버튼, +/- 버튼 기능
3. 더하기, 빼기 기능

생각보다 아이폰 계산기가 좀 특이하더라. 더하기 빼기로만 계산할 경우, + 버튼, - 버튼을 누르면 바로 계산 결과가 나왔다.
그래서 곱하기 나누기도 바로 전체 계산 결과가 나오는 줄 알았더니, 아니었다.

대충 예를 들어보면,
```
10 + 10 + 10 * 10 * 10 = 을 계산할 때 화면에 뜨는 숫자는 
10 / 20 / 10 / 100 / 1000 이렇게 나오고  
= 을 눌러야 1020 이렇게 나온다.
```  
좀 특이하긴 했지만 + - 보다 * / 연산을 먼저해야 하니까 어쩔 수 없구나 싶었다. 

그리고 + 버튼이나 - 버튼이 연속으로 눌리면 연산이 중복되기 때문에 버튼을 한번만 누를 수 있게 하는 법에 대해 새롭게 배웠다.

원래는 비슷한 프로젝트를 구상하고 코드도 비슷하게 작성하는 형식으로 공부했는데, 완전히 새로운 프로젝트를 해보니 너무 재밌었다.
또 프로젝트를 하면서 아직 내가 많이 부족하다는 것을 알게 되어 더 동기부여가 된 것 같다.각 버튼마다 계속 반복되는 기능을 어떻게 간단히 할 수 있을지 고민 좀 해봐야겠다.

**📌 버튼을 누를 수 있게/없게 하는 법**
```swift
// 1. 버튼을 아웃렛 변수로 선언
@IBOutlet weak var someButton: UIButton!

// 2. isUserInteractionEnabled 메서드 사용
someButton.isUserInteractionEnabled = true   // 누를 수 있게
someButton.isUserInteractionEnabled = false  // 누를 수 없게
```

## SUN
새로운 [이 블로그](http://eunjios.github.io) 를 만들었다.

원래는 미디엄으로 글을 종종 썼는데 아무래도 한국어 버전 글꼴이 좀 안 예쁘고, 글쓰기 양식도 한정적이라 새로 만들게 되었다.
이것도 열심히 써야겠다. 화이팅!
