# 객체란?

> 💡 `자바스크립트는 객체(object) 기반의 프로그래밍 언어`이며, 자바스크립트를 구성하는 거의 "모든 것"이 객체다.
>> 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체다.

>> 원시 타입의 값, 즉 `원시값은 변경 불가능한 값(immutable value)`이지만
객체 타입의 값, 즉 `개체는 변경 가능한 값(mutable value)`이다.
<br>

- **객체는 0개 이상의 프로퍼티로 구성된** 집합이며, **프로퍼티는 키(key)와 값(value)** 으로 구성된다.

```js

var person = {
  name: 'Lee',     // 프로퍼티 키 : name, 프로퍼티 값 : Lee
  age: 20          // 프로퍼티 키 : age, 프로퍼티 값 : 20
};

```
<br>

# 객체 리터럴에 의한 객체 생성

> 💡 `자바스크립트는 프로토타입 기반 객체지향 언어`로서
클래스 기반 객체지향 언어와는 달리 `다양한 객체 생성 방법을 지원`한다.
>> 1️. 객체 리터럴 2️. object 생성자 함수 3️. 생성자 함수 4️. Object.create 메서드 5️. 클래스(ES6)
<br>

### 객체 리터럴

> `객체 리터럴`은 `중괄호({ ... }) 내에 0개 이상의 프로퍼티를 정의`한다.
>> 변수에 할당되는 시점에 자바스크립트 엔진은 객체 리터럴을 해석해 객체를 생성한다.
<br>

```js

var person = {
  name: 'Lee',
  sayHello: function () {
    console.log(`Hello! My name is ${this.name}.`);
  }
};

console.log(typeof person); // object
console.log(person); // {name: "Lee", sayHello: f}

// 만약 프로퍼티를 정의하지 않으면 빈 객체가 생성된다.
var empty = {}; // 빈 객체
console.log(typeof empty); // object
```
<br>

- 주의할 것은, **객체 리터럴이 값으로 평가되는 표현식**이며, **중괄호는 코드 블록을 의미하지 않는다.**
  - 따라서 객체 리터럴의 닫는 중괄호 뒤에는 세미콜론(;)을 붙여야 한다.
<br>

# 프로퍼티

> 💡 객체는 프로퍼티의 집합임, 프로퍼티는 키와 값으로 구성된다.
>> `프로퍼티 키` : 빈 문자열을 포함하는 모든 문자열 또는 심벌 값

>> `프로퍼티 값` : 자바스크립트에서 사용할 수 있는 모든 값
<br>

```
🔎 Note

프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로서 식별자 역할을 한다.
또한 프로퍼티 키의 네이밍을 할 때, 반드시 식별자 네이밍 규칙을 따라야 하는 것은 아니다.

그러나 자바스크립트에서 사용 가능한 유효한 이름인 경우 따옴표를 생략할 수 있지만
식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다!
```
<br>

# 메서드

> 💡 `프로퍼티 값이 함수`일 경우 일반 함수와 구분하기 위해 `메서드(method)`라 부른다.
>> 즉, 메서드는 객체에 묶여 있는 함수를 의미한다.


```js

var circle = {
  radius: 5, // 프로퍼티

  // 원의 지름
  getDiameter: function () { // 메서드
    return 2 * this.radius;  // this 는 circle을 가리킨다.
  }
};

console.log(circle.getDiameter()); // 10
```
<br>

# 프로퍼티 접근

> 💡 자바스크립트에서 제공하는 `프로퍼티 접근 방법`은 두 가지가 있다.
<br>

## 1️⃣ 마침표 표기법

> 마침표 프로퍼티 접근 연산자(.)의 `좌측에는 객체로 평가되는 표현식`을 기술하며, `우측에는 프로퍼티 키`를 지정한다.

```js

// 마침표 표기법에 의한 프로퍼티 접근
var person = {
  name: 'Lee'
};

console.log(person.name); // Lee

```
<br>

## 2️⃣ 대괄호 표기법
> 대괄호 프로퍼티 접근 연산자([ ... ])의 `좌측에는 객체로 평가되는 표현식`을 기술하며, `내부에는 프로퍼티 키`를 지정한다.
>> 또한 대괄호 프로퍼티 접근 연산자 내부에 지정하는 `프로퍼티 키는 반드시 따옴표로 감싼 문자열`이어야 한다.

>> 또한, 자바스크립트에서 `사용 가능한 유효한 이름이 아니면 반드시 대괄호 표기법을 사용`해한다.

```js

var person = {
  name: 'Lee',
  'last-name': 'Lee'
};

console.log(person['name']); // Lee


// 프로퍼티 키를 따옴표로 감싸지 않았을 때
// 식별자를 찾지 못해 ReferenceError가 발생한다.
console.log(person[name]); // ReferenceError: name is not defined

// 프로퍼티 키가 객체에 존재하지 않을 때
// undefined를 반환하며, ReferenceError가 발생하지 않는다.
console.log(person['age']); // undefined

// 사용 가능한 유효한 이름이 아닐 때는 대괄호 표기법을 사용하자!
console.log(person.'last-name'); // SyntaxError: Unexpected string
console.log(person.last-name); // NaN
console.log(person['last-name']); // Lee

```
<br>

# 프로퍼티 값 갱신
<br>

# 프로퍼티 동적 생성
<br>

# 프로퍼티 삭제
<br>

# ES6에서 추가된 객체 리터럴의 확장 기능
<br>

## 1️⃣ 프로퍼티 축약 표현
<br>

## 2️⃣  계산된 프로퍼티 이름
<br>

## 3️⃣ 메서드 축약 표현




