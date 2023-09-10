# 생성자 함수

> 💡 `생성자 함수(constructor)` : new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수
>> 생성자 함수에 의해 생성된 객체를 `인스턴스(instance)`라 한다.
<br>

## Object 생성자 함수

> new 연산자와 함께 `Object 생성자 함수를 호출`하면 빈 객체를 생성하여 반환한다.
<br>

```js

// 빈 객체의 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function (0 {
  console.log('Hi, My name is ' + this.name);
};

console.log(person); // {name: "Lee", sayHello: f}
person.sayHello(); // Hi! My name is Lee

```
<br>

- Object 생성자 함수 이외에도
String, Number, Boolean, Function, Array, Date, RegExp, promis 등 `빌트인(built-in) 생성자 함수를 제공`

```js

// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee');
console.log(typeof strObj);  // object
console.log(strObj);         // String {"Lee"}

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123);

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj = new Boolean(true);

// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x');
console.log(typeof func);  // function

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3);

// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
const regExp = new RegExp(/ab+c/i);

// Date 생성자 함수에 의한 Date 객체 생성
const date = new Date();

```
<br>

## 생성자 함수를 쓰는 이유

### 1️⃣ 객체 리터럴에 의한 객체 생성 방식의 문제점
> `동일한 프로퍼티를 갖는 객체를 여러 개 생성해야하는 경우` 매번 같은 프로퍼티를 기술해야 하기 때문
<br>

```js

const circle1 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle1.getDiameter()); // 10

const circle2 = {
  radius: 10,
  getDiameter() {
    return 2 * this.radius;
  }
};

console.log(circle2.getDiameter()); // 20

```
<br>

- 객체는 `프로퍼티를 통해 객체 고유의 상태(state)를 표현`하며,
- `메서드를 통해 상태 데이터인 프로퍼티를 참조하고 조작하는 동작(behavior)을 표현`한다.

+ ⇒ 객체마다 프로퍼티 값이 다를 수 있지만 **메서드는 내용일 동일한 경우가 일반적!**
  + 이는 수십 개의 객체를 생성할 때 `효율을 하락`시킨다.
<br>

### 2️⃣ 생성자 함수에 의한 객체 생성 방식의 장점

> 프로퍼티 구조가 동일한 `객체 여러 개를 간편하게 생성`할 수 있다.
>> 객체 하나 하나 정의하지 않고, `하나의 인스턴스로 틀을 생성`한다는 의미다.
<br>

```js

function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성
const circle2 = new Circle(10); // 반지름이 10인 Circle 객체를 생성

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20

```
<br>

```js
🔎 Note

[this가 가리키는 다양한 값(this 바인딩)]

"this" : 객체 자신의 프로퍼티나 메서드를 참조하기 위한 "참조 변수(self-referencing variable)"다.
this가 가리키는 값은 함수 호출 방식에 따라 "동적으로 결정"된다.


|    함수 호출 방식     |                 this 값                |
| 일반 함수로서 호출    | 전역 객체                              |
| 메서드로서 호출       | 메서드를 호출한 객체(마침표 앞의 객체)   |
| 생성자 함수로서 호출  | 생성자 함수가 (미래에) 생성할 인스턴스   |
```
<br>

```js
🔎 Note

[생성자 함수(인스턴스) 내부에서 this의 의미!]

function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

위 예제에서 this가 의미하는 것,,??

이는 "생성자 함수가 (미래에) 생성할 인스턴스"를 의미한다.

→ this.radius → circle1.radius
circle1. radius = 5;
circle1.getDiameter = function() ...

"Object 생성자 함수를 사용하지 않았을 때" 원 형식
⇒  const circle1 = {
      radius = 5;
      getDiameter() {
        return 2 * this.radius;
      }
    };
→ 이걸 간편하게 한 것이 인스턴스 내부에서 this 를 사용하여 작성한 것이다.
```
<br>

## 생성자 함수의 인스턴스 생성 과정

> `생성자 함수의 역할` : 1. 인스턴스를 생성 2. 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)
>> 인스턴스를 생성하는 것 ⇒ `필수` & 생성된 인스턴스를 초기화하는 것 ⇒ `옵션`
<br>

### 1️⃣ 인스턴스 생성과 this 바인딩
<br>

### 2️⃣ 인스턴스 초기화
<br>

### 3️⃣ 인스턴스 반환
<br>

## 내부 메서드 [[Call]] & [[Construct]]
<br>

### construct & non-constructor 구분
<br>

## new 연산자
<br>

## new.target
