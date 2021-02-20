---
title: "[Swift] Structure (구조체) 문법 정리"
excerpt: "구조체의 문법을 정리해보자."
date: 2021-02-18 01:34:00 -0400
category: Syntax
---

> CATEGORY - Syntax
> 스위프트 문법을 정리합니다. 

# 📌 Structure (구조체) 란?
구조체는 클래스와 같이 객체지향 언어를 위한 필수적인 요소로 프로그램의 코드를 추상화하기 위해 사용됩니다. 구조체의 구성은 프로퍼티(property)와 메서드(method)로 이루어져있습니다. 프로퍼티는 구조체 내부의 변수, 메서드는 구조체 내부의 함수로 생각하면 됩니다. 

<br>

## 1. 구조체 만들기
구조체는 `struct` 키워드를 사용하여 다음과 같이 만들 수 있습니다. 구조체는 스위프트에서 타입을 지정하는 것으로 대문자로 구조체의 이름을 만들어줍니다.
```swift
struct StructName {
	// code...
}
```

위 문법을 사용하여 구조체를 만들어 볼까요?
```swift
struct SomeStuctName {
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
위 코드와 같이 구조체를 만들 수가 있습니다. 여기서 프로퍼티는 인스턴스 프로퍼티와 타입 프로퍼티로 나뉘고, 메서드도 인스턴스 메서드와 타입 메서드로 나뉩니다. 
* **Instance property/method**: 인스턴스 내에서 사용하는 프로퍼티/메서드 입니다.
* **Type property/method**: 타입 내에서 사용하는 프로퍼티/메서드 입니다. `static` 키워드를 사용하면 타입 내에서 사용하는 프로퍼티/메서드를 만들 수 있습니다.

<br>

## 2. 인스턴스 생성하기
위에서 만든 구조체는 틀이라고 생각하면 되는데요. 구조체만 생성할 경우, 오직 틀만 존재하는 것이고 그 실체는 아직 없는 것 입니다. 따라서 실체, 즉 인스턴스를 생성하여 사용해야 합니다. 인스턴스는 다음과 같이 생성할 수 있습니다.

### `var` 키워드를 사용하여 인스턴스 생성하기
```swift
var mutableInstance: SomeStructName = SomeStructName()
```

이렇게 타입을 `SomestuctName` 으로 지정하면 인스턴스를 생성할 수 있습니다. 또 내부 프로퍼티 값을 바꿀 때는 다음과 같이 바꿀 수 있습니다. 여기서 주의할 점은 구조체를 생성할 때, `let` 키워드를 사용한 불변 프로퍼티는 값을 바꿀 수가 없다는 것 입니다. 
```swift
mutableInstance.mutableProperty = 20
// mutableInstance.immutableProperty = 20
```
즉, `mutableInstance.immutableProperty = 20` 를 실행하면, `Cannot assign to property: 'immutableProperty' is a 'let' constant` 라는 컴파일 오류가 발생합니다.

만약 특정 값을 변경하여 인스턴스를 생성하고 싶으면 다음과 같이 만들 수도 있습니다.
```swift
var mutableInstance = SomeStructName(mutableProperty: 20)
```
<br>

### `let` 키워드를 사용하여 인스턴스 생성하기
```swift
let immutableInstance: SomeStructName = SomeStructName()
```
`let` 키워드를 사용해도 동일한 방법으로 인스턴스를 생성할 수 있습니다. 다만 `let` 키워드를 사용했기 때문에 인스턴스를 생성한 후에는 불변 프로퍼티, 가변 프로퍼티 모두 값을 바꿀 수 없습니다.

```swift
immutableInstance.mutableProperty = 20
immutableInstance.immutableProperty = 20
// 두 경우 모두 컴파일 오류 
```
위의 두 경우 모두 `Cannot assign to property: 'immutableInstance' is a 'let' constant` 라는 컴파일 오류가 발생합니다. 

반면, 인스턴스의 초기값을 변경하여 생성하는 것 또한 가능합니다. 
```swift
let immutableInstance = SomeStructName(mutableProperty: 20)
```
이 경우에는 구조체에 정의된 프로퍼티 값과 다른 값을 갖는 인스턴스를 생성할 수 있습니다. 다만 생성 이후에 프로퍼티 값을 변경할 수는 없습니다.
```swift
immutableInstance.mutableProperty = 30
immutableInstance.immutableProperty = 30
// 두 경우 모두 컴파일 오류 
```

<br>

## 3. 타입 프로퍼티? 타입 메서드?
앞서 [구조체 만들기](#1-구조체-만들기) 에서 잠깐 언급을 했는데 한 번 더 정리해봅시다. `var`, `let`, `func` 키워드 앞에 `static` 키워드를 쓰면 타입 프로퍼티, 타입 메서드를 만들 수 있다고 했는데, 타입 프로퍼티와 타입 메서드는 무엇일까요?

타입 프로퍼티/메서드는 인스턴스 내에서 쓰는 프로퍼티/메서드가 아닌 타입 내에서 쓰는 프로퍼티/메서드 입니다. 예를 들어보면 다음과 같습니다.

```swift
print(mutableInstance.typeProperty)		// error
print(SomeStructName.typeProperty)		// 10
```
이처럼 인스턴스인 `mutableInstance` 로 `typeProperty` 를 접근하려고 하면 오류가 생기고, 스트럭처 타입인 `SomeStructName` 으로 접근해야 합니다. 타입 메서드도 타입 프로퍼티와 동일한 방식으로 `SomeStructName.typeMethod()` 와 같이 접근해야 합니다.

<br>

## 4. `mutating` 키워드를 사용한 메서드
먼저 지금까지 배웠던 내용을 이용해 학생이라는 구조체를 한 번 만들어보도록 하겠습니다. 
```swift
struct Student {
	var name: String = "unknown"
	var score: Int = 0

	func study() {
		print("열심히 공부하는 중")
	}
}
```

위의 코드를 통해 `Student` 라는 구조체를 만들었습니다. 위 구조체에서 내부의 프로퍼티를 변경하는 메서드는 어떻게 만들 수 있을까요? 한 번 앞서 만든 `Student` 구조체 내부의 `study()` 메서드를 수정해봅시다. 해당 메서드를 실행하면 현재 `score` 에 10 이 더해지도록 구현해볼까요?

그냥 똑같이 `func` 키워드를 사용해서 만들면 되는거 아닌가? 라는 생각이 들지만, 구조체 내부의 프로퍼티 값을 변경하는 메서드를 만들기 위해서는 `mutating` 이라는 키워드가 필수적 입니다. 즉, 다음과 같이 코드를 수정해야 합니다.
```swift
struct Student {
	var name: String = "unknown"
	var score: Int = 0

	mutating func study() {
		score += 10
		if score >= 100 {
			score = 100
		}
		print("열심히 공부하는 중...")
	}
}
```

<br>

## 5. 함수의 input type 을 구조체로 설정하기
구조체는 타입처럼 사용이 되기 때문에 함수의 입력값의 타입을 구조체로 지정할 수 있습니다. 

그럼 한 번 함수를 만들 때, 방금 만든 구조체인 `Student` 를 입력 타입으로 갖도록 하고, 학생의 점수가 80점 보다 낮으면 "열심히 공부 합시다." 를 출력하는 함수를 만들어 봅시다.

```swift
func shouldStudy(_ student: Student) {
	if student.score < 80 {
		print("점수가 \(student.score)점 이네요. 열심히 공부 합시다.")
	} else {
		print("점수가 \(student.score)점 이네요. 열심히 하고 있네요")
	}
}
```

위 코드와 같이 함수의 입력 타입을 `String`, `Int` 등의 타입 뿐만이 아닌 구조체로 지정해줄 수 있습니다.
 
<br>

## 6. `extension` 키워드를 사용하여 메서드 추가하기
마지막으로 `extension` 키워드를 사용하여 구조체의 메서드를 추가하는 방법에 대해 정리해보도록 하겠습니다.

이미 스위프트에서는 `Int` 타입을 구조체로 정의해 두었는데 우리가  `extension` 을 사용하면 `Int` 내부의 메서드를 추가할 수도 있습니다. 한번 해당 숫자에 제곱을 출력하는 메서드를 추가해 볼까요?

```swift
extension Int {
	func square() -> Int {
		return self * self
	}
}
```
이렇게 추가할 수 있고 사용은 다음과 같이 할 수 있습니다.
```swift
let value = 2
value.square()		// 4
3.square()		// 9
```

<br>

<hr>
그럼 오늘은 여기까지 구조체를 정리하고, 다음에는 클래스의 문법을 정리하도록 하겠습니다! 🤓
