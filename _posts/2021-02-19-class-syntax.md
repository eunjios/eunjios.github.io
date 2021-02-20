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

<br>

## 5. 클래스를 상속받기
클래스를 생성할 때 다른 클래스를 상속 받아서 사용할 수도 있습니다. 스위프트의 상속의 몇 가지 규칙을 정리해보면 다음과 같습니다.
* 클래스만 상속을 받을 수 있고 구조체는 상속 불가능
* 서브 클래스는 하나의 슈퍼 클래스만 상속 받을 수 있음
* 슈퍼 클래스는 여러개의 서브 클래스를 가질 수 있음
* 상속의 깊이는 상관 없음

슈퍼 클래스로부터 상속을 받는 법은 간단합니다. 클래스를 생성할 때 `: SuperClassName` 만 추가하면 됩니다.
```swift
class SubClassName: SuperClassName {
	// 구현부 
}
```

이제 어떻게 상속을 받는지 알았으니까 예시를 들어볼까요?

먼저 슈퍼 클래스인 `Person` 을 만들어 봅시다. (동일하게 클래스를 생성하면 됩니다.)

```swift
class Person {
	var firstName: String
	var lastName: String
	
	init(firstName: String, lastName: String) {
		self.firstName = firstName
		self.lastName = lastName
	}

	func printMyName(){
		print("my name is \(firstName) \(lastName)")
	}
}
```
이번에는 `Person` 클래스를 상속받는 `대학생` 이라는 클래스를 만들어 볼까요? (스위프트는 유니코드를 지원하기 때문에 이름을 정할 때 한글로 정해도 됩니다.)
```swift
class 대학생: Person {
	var univName: String
	var major: String

	init(firstName: String, lastName: String, univName: String, major: String) {
		self.univName = univName
		self.major = major
		super.init(firstName: firstName, lastName: lastName)
	}
}
```
잠깐 복습하면 초기값 설정을 안 해줬기 때문에 `init()` 을 사용해야 하는 것 인데요. 

**여기서 주의할 점!!** `대학생` 클래스가 상속받은 `Person` 이라는 클래스도 생성자가 있었기 때문에 `init()`  내부에 `super.init()` 도 필수적으로 설정해줘야 합니다.

여기까지 하면 `대학생` 클래스는 성공적으로 `Person` 클래스를 상속 받을 수 있습니다. 즉, `Person` 클래스 내부에 있던 프로퍼티와 메소드를 모두 사용할 수 있는거죠. 그럼 이제 인스턴스를 생성해볼까요?

```swift
let someOne = 대학생(firstName: "Name", lastName: "Lee", univName: "univ", major: "major")

print(someOne.firstName)	// Name
print(someOne.univName)		// univ
someOne.printMyName()		// my name is Name Lee
```
<br>

### 👀 조금 더 어려운 걸 해봅시다.
이번에는 `대학생` 클래스에 GPA 를 나타내는 배열을 프로퍼티로 추가해 볼 예정인데요. 이전 시간에 구조체를 배웠으니까, 배열의 값은 학기와 GPA 데이터를 갖는 구조체로 만들어 봅시다. 

1. 먼저 `GPABySemester` 라는 구조체를 생성해 줍니다.
	```swift
	struct GPABySemester {
		var semester: Int
		var gpa: Double
	}
	```
	참고로 구조체는 생성자가 없어도 됩니다. 저절로 memberwise initializer 가 생성되기 때문입니다.

2. `대학생` 클래스에 `gpa` 프로퍼티를 추가합니다. 이 때   `GPABySemester` 의 타입을 가지는 빈 배열로 설정해줍시다. 초기값을 줌으로써 `생성자(init)` 를 사용할 필요가 없습니다! *(편의상 다른 프로퍼티는 다 생략 했습니다.)*
	```swift
	class 대학생: Person {
		var gpa: [GPABySemester] = []
	}
	```
3. `대학생` 클래스의 인스턴스를 생성합니다.
	```swift
	let someStudent = 대학생(firstName: "Name", lastName: "Lee")
	```
4. `GPAByGrade` 구조체의 인스턴스를 생성합니다.
	```swift
	let firstGPA = GPABySemester(semester: 1, gpa: 4.4)
	let secondGPA = GPABySemester(semester: 2, gpa: 4.5)
	let thirdGPA = GPABySemester(semester: 3, gpa: 4.0)
	```
5. 위의 인스턴스들을 `someStudent` 의 `gpa` 배열에 추가해주면?
	```swift
	someStudent.gpa.append(firstGPA)
	someStudent.gpa += [sencondGPA, thirdGPA]
	```
	저는 한 번 두가지 경우로 배열을 추가해 보았습니다. 참고로 여기서 `someStudent` 는 `let` 키워드를 사용하여 생성 했는데, 잘못 된 거 아니냐? 생각할 수 있지만, 이는 클래스의 인스턴스기 때문에 내부의 가변 프로퍼티 값을 바꿀 수 있는 것 입니다.
<br>

### 🤔 상속을 언제 어떻게 써야 할까?
상속은 중복되는 코드를 줄일 수 있다는 점에서 좋습니다. 그렇지만 너무 많이 써서 상속의 깊이가 너무 깊어진다면 유지보수가 힘들어진다는 단점이 있습니다. 그럼 상속을 언제 어떻게 써야 할까요?

1. 부모/자식 클래스를 명확히 구분해야 할 때 상속을 사용하자.
2. 객체 자체의 정체성을 구현하고 싶을 때 부모 클래스로부터 상속 받아 객체를 만들자.
3. 비슷하지만 다른 내용을 다룰 때 상속을 고려하여 다양한 구현을 가능하게 하자.
4. 외부 앱에서 필요로 할 때, 즉 확장성이 필요할 때 상속을 사용하자.
5. 각 클래스는 한 개의 고려 사항만 있도록하여 정확한 정체성을 갖게 하자. 너무 많은 걸 하나의 클래스가 사용하려고 하면 안된다. (유지보수에 어려움)

<hr>

그럼 오늘은 여기까지 문법을 정리하고, 다음 시간에는 구조체와 클래스의 차이를 중점적으로 포스팅 하겠습니다. 🤓


