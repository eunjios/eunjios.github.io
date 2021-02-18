---
title: "[Swift] Class (클래스) 문법 정리"
excerpt: "클래스의 문법을 정리해보자."
date: 2021-02-19 01:39:00 -0400
category: Syntax
---

> CATEGORY - Syntax  
> 스위프트 문법을 정리합니다.

# 📌 Class (클래스) 란?
클래스는 구조체와 거의 비슷한 문법을 가지며, 객체지향 언어를 위한 필수적인 요소로서 사용됩니다. 클래스의 구성 역시 프로퍼티(property)와 메서드(method)로 이루어져있습니다. 프로퍼티는 클래스 내부의 변수, 메서드는 클래스 내부의 함수로 생각하면 됩니다. 

## 1. 클래스 만들기

클래스는 `class` 키워드를 사용하여 다음과 같이 만들 수 있습니다. 클래스는 스위프트에서 일종의 타입을 지정하는 것과 같으므로 대문자로 클래스의 이름을 만들어줍니다.
```swift
class ClassName {
	// 구현부 
}
```
위 문법을 사용하여 클래스를 만들어 보면 다음과 같습니다.
```swift
class SomeClassName {
	// 프로퍼티
	var mutableProperty: Int = 10
	let immutableProperty: Int = 10
	static var typeProperty: Int = 10

	// 메서드
	func instanceMethod() {
		print("Hello")
	}
	static func typeMethod() {
		print("World")
	}
}
```

클래스의 프로퍼티와 메서드는 구조체와 동일하게 인스턴스, 타입으로 나뉩니다. 그렇기 때문에 클래스를 생성할 때의 구현부는 구조체와 동일하게 작성하면 됩니다. 

### 프로퍼티의 초기값을 설정해주지 않는 경우
앞서 클래스를 만들 때 각 프로퍼티의 값을 지정해주었는데, 만약 초기값을 특정 값으로 설정해주기 싫다면 클래스를 어떻게 만들 수 있을까요?
```swift
class SomeClassName {
	var mutableProperty: Int
	let immutableProperty: Int
}
```
이렇게 만들고 싶으면 무조건 `init` 키워드를 통해 initializer를 지정해주어야 합니다. (사실 구조체도 동일합니다!)
```swift
class SomeClassName {
	var a: Int			// init 필수
	var b: Int = 1		// init 해도 되고 안해도 됨 
	let c: Int			// init 필수

	init(a: Int, c: Int) {
		self.a = a
		self.c = c
	}
}
```

그러나 인스턴스를 생성한 후 프로퍼티를 바꿀 때 코드의 <u>실행 결과</u>는 구조체와 조금 다릅니다. 아래 인스턴스를 생성하여 코드의 실행 결과를 살펴 볼까요?

<br>

## 2. 인스턴스 생성하기
위에서 만든 클래스의 인스턴스를 생성해 봅시다. 인스턴스를 생성할 때도 구조체와 동일한 방식을 사용하면 됩니다.

### `var` 키워드를 사용하여 인스턴스 생성하기
```swift
var mutableInstance: SomeClassName = SomeClassName()
```
`var` 키워드를 사용하여 인스턴스를 생성했습니다. 만약 인스턴스 내부의  프로퍼티 값을 바꾸고 싶다면 다음과 같이 코드를 작성할 수 있습니다.

```swift
mutableInstance.mutableProperty = 20
// mutableInstance.immutableProperty = 20 -> error
```
<u>여기서 주의 할 점!</u> 클래스 내부의 `mutableProperty` 의 값만 변경이 가능합니다. `let` 키워드를 사용한 인스턴스 프로퍼티는 값을 변경할 수 없습니다. (여기까지는 구조체와 동일하죠?)
<br>

### `let` 키워드를 사용하여 인스턴스 생성하기
앞 내용은 사실 키워드가 `struct` 에서 `class` 로 바뀐 것 외에는 구조체와 별반 다를게 없었는데요. `let` 을 사용해 인스턴스를 생성하는 경우에서 차이가 생깁니다. 
```swift
let immutableInstance: SomeClassName = SomeClassName()
```
`let` 키워드를 사용하여 인스턴스를 생성하였습니다. 만약 인스턴스 내부의  프로퍼티 값을 바꾸고 싶다면 다음과 같이 코드를 작성할 수 있습니다.

```swift
mutableInstance.mutableProperty = 20
// mutableInstance.immutableProperty = 20 -> error
```
자 이제 여기에서 구조체와의 차이가 생기는데요. 구조체의 인스턴스를 `let` 을 통해 한 번 생성하게 되면, 이후에는 인스턴스 프로퍼티의 값을 바꿀 수가 없었습니다. 그러나 클래스의 인스턴스를 `let` 으로 생성해도 가변 인스턴스 프로퍼티 일 경우에는 이후에 프로퍼티의 값을 바꿀 수가 있습니다.
<br>

### 초기값을 가지는 클래스 인스턴스 생성하기
잠깐 이전 내용을 복습하면, 초기값을 가지는 구조체의 인스턴스는 다음과 같이 만들 수 있었습니다.
```swift
var instance = StructName(property: value)
```

그렇다면, 초기값을 가지는 클래스의 인스턴스는 어떻게 만들 수 있을까요?
이 때는 `init` 을 사용해야만 인스턴스 생성시에 초기값을 지정해줄 수 있습니다.
```swift
// 클래스 생성
class Student {
	var isStudent: Bool = true
	var name: String
	var score: Int = 0

	init(name: String, score: Int){
		self.name = name
		self.score = score
	}
}

// 인스턴스 생성
var student = Student(name: "Eunji", score: 100)
// var student = Student() -> error
```
위 코드와 같이 `init` 의 인풋인 `name` 과 `score` 만을 지정해줄 수 있습니다. 만약 `name` 과 `score` 의 값을 지정해주지 않으면 오류가 발생합니다.

<br>

## 3. `mutating` 키워드?
구조체의 경우, 내부 프로퍼티의 값을 바꾸는 메서드는 `mutating func` 키워드를 사용했는데요. 

클래스는 `mutating` 키워드가 필요 없습니다. 그냥 `func` 키워드만 사용하면 내부 프로퍼티의 값을 바꿀 수 있습니다.

<br>

## 4. 함수의 input type 을 클래스로 설정하기
이 부분은 구조체와 동일하기 때문에 해당 내용은 간단한 예시 정도만 보도록 하겠습니다. [자세한 내용은 이 링크를 참고하세요!](https://eunjios.github.io/syntax/structure-syntax/)

```swift
func printStudentInfo(_ student: Student) {
	print("저는 \(student.name) 입니다.")
	print("점수는 \(student.score)점 입니다")
}

printStudentInfo(student)
// 저는 Eunji 입니다.
// 점수는 100점 입니다.
```
이런 식으로 함수의 인풋 타입을 클래스로 지정해줄 수도 있습니다.

<hr>

그럼 오늘은 여기까지 문법을 정리하고, 다음 시간에는 구조체와 클래스의 차이를 중점적으로 포스팅 하겠습니다. 🤓

