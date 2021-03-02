---
title: "[Swift] 구조체 VS 클래스"
excerpt: "구조체와 클래스 어떤 차이가 있는지 정리해보자."
date: 2021-03-02 14:17:00 -0400
category: Syntax
---

> CATEGORY: Syntax  
> 스위프트 문법을 정리합니다.

# 📌 구조체 VS 클래스
저번 시간에는 구조체와 클래스 문법에 대해 정리했는데, 둘은 매우 비슷하지만 약간의 차이점이 있었죠? 따라서 이번 시간에는 왜 이런 차이가 생기는지에 대해 살짝 정리하고 이로 인해 생기는 차이점에 대해 배워보도록 하겠습니다.
<br>
<br>

## 0. 문법 정리하며 달랐던 점을 정리해보자.

| |구조체|클래스|
|---|---|---|
|initializer|initializer가 없어도 가능|initailizer 필수|
|mutating|구조체 내부의 프로퍼티의 값을 바꾸기 위해선 mutating 필수|클래스 내부의 프로퍼티 값을 바꿔도 mutating 사용할 필요 없음|
|let 인스턴스|가변 프로퍼티여도 값을 바꿀 수 없음|가변 프로퍼티면 값을 바꿀 수 있음|
|상속|불가능|가능|
<br>
<br>

## 1. 밸류 타입  VS  레퍼런스 타입

* <u>구조체</u>: 밸류 타입 (value type) 
* <u>클래스</U>: 레퍼런스 타입 (reference type)

밸류 타입이란 구조체가 복사되는 형태, 레퍼런스 타입이란 구조체를 참조하는 형태 (쉽게 말해 포인팅을 하고있음)를 말합니다. 직접 해보면 훨씬 이해가 잘 되기 때문에 한 번 예시를 들어보겠습니다.
<br>

### 구조체
먼저 구조체를 만들어 봅시다.
```swift
struct InfoStruct {
	var name: String
	var age: Int
	
	func printInfo {
		print("name: \(name), age: \(age)")
	}
}
```

구조체의 인스턴스를 만들어 봅시다.
```swift
var user1 = InfoStruct(name: "Eunji", age: 23)
var user2 = user1
user2.name = "Gwan"
user2.age = 24
```
`printInfo()` 메서드를 사용하여 각 인스턴스의 이름과 나이를 출력해 봅시다.
```swift
user1.printInfo()		// name: Eunji, age: 23
user2.printInfo() 		// name: Gwan, age: 24
```

이처럼 value type은 인스턴스를 생성할 때 각각의 구조체로 복사되기 때문에 원래의 구조체 인스턴스 `user1` 과 `user2` 는 다른 값을 가질 수 있는 것 입니다. (참고로 수정이 일어날 때 값이 복사됩니다.)
<br>

### 클래스
그럼 이제 클래스의 레퍼런스 타입에 대해 알아봅시다. 먼저 클래스를 만들어 보면,
```swift
class InfoClass {
	var name: String
	var age: Int
	
	init(name: String, age: Int) {
		self.name = name
		self.age = age
	}
	
	func printInfo {
		print("name: \(name), age: \(age)")
	}
}
```
이렇게 만들 수 있고, 클래스는 initializer가 무조건 필요하기 때문에 `init` 키워드를 사용하여 초기값을 지정해 줍니다.

그럼 이제 구조체의 인스턴스를 만들어 봅시다.
```swift
var user3 = InfoClass(name: "Eunji", age: 23)
var user4 = user3
user4.name = "Gwan"
user4.age = 24
```
`printInfo()` 메서드를 사용하여 각 인스턴스의 이름과 나이를 출력해 봅시다.
```swift
user3.printInfo()		// name: Gwan, age: 24
user4.printInfo() 		// name: Gwan, age: 24
```

reference type은 value type 과는 다르게 인스턴스 `user3` 과 `user4` 가 같은 값을 가지게 됩니다. 이는 클래스를 복사해 오는 것이 아닌 같은 클래스를 가리키고 있기 때문입니다.
<br>
<br>

## 2. Stack  VS  Heap
이번에는 메모리 측면에서 비교를 해보겠습니다.
* <u>구조체</u>: Stack
* <u>클래스</u>: Heap

### Stack
* RAM 에 해당하는 메모리 공간
* 효율적이다.
* 상대적으로 빠르다.
* 자동으로 데이터가 삭제되고 관리된다.
* 스택 변수는 함수가 실행되는 동안에만 존재한다.

### Heap
* RAM 에 해당하는 메모리 공간
* 상대적으로 느리다.
* 자동으로 데이터가 삭제되거나 관리되지 않는다.
<br>
<br>

# 🤔 그럼 언제 구조체를 사용하는게 좋을까?

스위프트는 구조체를 좋아한다. 때문에 웬만한 객체는 구조체를 사용하되 이후에 클래스가 필수적인 경우에만 클래스로 바꿔서 사용하자.

## 👀 이럴 때 구조체를 사용하자!
1. 두 객체의 데이터를 같다/다르다 로 비교해야 하는 경우
2. 복사된 두 객체가 독립적인 상태를 가져야 하는 경우 
3. 코드에서 객체의 데이터를 여러 스레드에 걸쳐 사용해야 하는 경우

## 👀 이럴 때 클래스를 사용하자!
1. 두 객체의 인스턴스 자체가 같음을 확인해야 하는 경우
2. 하나의 유일한 객체가 여러 대상에 의해 접근되거나 변경될 수 있어야 하는 경우
