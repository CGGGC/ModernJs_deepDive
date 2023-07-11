# 데이터 타입

> 💡 데이터 타입(data type)은 `값의 종류`를 말한다.

- 자바스크립트의 `모든 값은 데이터 타입을 갖는다.`
  - 이때 자바스크립트(ES6)는 `7개의 데이터 타입을 제공`하며,
    이는 `원시 타입(primitive type)과 객체 타입(object/reference type)으로 분류`할 수 있다.

| 구분        | 데이터 타입                | 설명                                                    |
|------------ |----------------------------|---------------------------------------------------------|
| 원시 타입    | 숫자(number) 타입          | 숫자. 정수와 실수 구분 없이 하나의 숫자 타입만 존재         |
|             | 문자열(string) 타입         | 문자열                                                  |
|             | 불리언(boolean) 타입        | 논리적 참(true)과 거짓(false)                            |
|             | undefined 타입             | var 키워드로 선언된 변수에 암묵적으로 할당되는 값           |
|             | null 타입                  | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값           |
|             | 심벌(symbol) 타입          | ES6에서 추가된 7번째 타입                                 |
| 객체 타입    |                           | 객체, 함수, 배열 등                                       |
<br>

# 숫자 타입

> 💡 자바스크립트는 독특하게 `하나의 숫자 타입만 존재`한다.

- `숫자 타입의 값`은 배정밀도 64비트 `부동소수점 형식`을 따른다.
  - `모든 수를 실수로 처리`하며, 정수만 표현하기 위한 데이터 타입이 별도로 존재하지 x

```
🔎 explanation

C나 자바의 경우 정수와 실수를 구분하여, int, long, float, double 등과 같은 다양한 숫자 타입을 제공한다.
```
<br>

```js
// 모두 10진수로 해석
var binary = 0b01000001; // 2진수
var octal = 0o101; // 8진수
var hex = 0x41; // 16진수

console.log(binary === octal); // true
console.log(octal === hex); // true
```
<br>

- `세 가지 특별한 값도 표현`할 수 있다.
  - Infinity: 양의 무한대
  -  -Infinity: 음의 무한대
  -   NaN: 산술 연산 불가(not-a-number)

```js
console.log(10 / 0); // Infinity
console.log(10 / -0); // -Infinity
console.log(1 * 'String'); // NaN
```
<br>

# 문자열 타입

> 💡 문자열(string)타입은 텍스트 데이터를 나타내는 데 사용한다.

- 자바스크립트의 `문자열은 원시 타입`이며, `변경 불가능한 값(immutable value)`이다.
  - 이것은 문자열이 생성되면 그 문자열을 변경할 수 없다는 것을 의미.
- `작은따옴표(''), 큰따옴표(""), 백틱(``)`으로 텍스트를 감싼다.
<br>

# 템플릿 리터럴

> 💡 ⭐템플릿 리터럴(templateliteral)은 `멀티라인 문자열(multi-line string), 표현식 삽입(expression interpolation),
태그드 템플릿(tagged template)` 등 편리한 `문자열 처리 기능을 제공`한다.

```
⭐ explanation

일반 문자열과 비슷해보이는 템플릿 리터럴은 문자열 타입 중 백틱(``)을 사용해 표현한다.
```

### 일반 문자열과 멀티라인 문자열

- `일반 문자열` 내에서는 `줄바꿈(개행)이 허용되지 않으며,`
  `공백을 표현`하기 위해 `이스케이프 시퀸스(escape sequence)를 사용`해야한다.

```js
// 일반 문자열 내에서는 줄바꿈(개행)이 허용되지 않는다.
var str = 'Hello
world.';
// SyntaxError: Invalid or unexpected token

// 이는 공백을 표현하기위해 이스케이프 시퀸스(escape sequence)를 사용해야한다.
var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>';

console.log(template);
// 출력 결과
// <ul>
//   <li><a href="#">Home</a></li>
// </ul>
```

- 이와 달리, 템플릿 리터럴이 제공하는 멀티라인 문자열 내에서는 줄바꿈이 허용된다.

```js
var template = '<ul>
  <li><a href="#">Home</a></li>
</ul>';

console.log(template);
// 출력 결과
// <ul>
//   <li><a href="#">Home</a></li>
// </ul>
```

### 표현식 삽입

- 문자열은 `문자열 연산자 +를 사용해 연결`할 수 있다.

```js
var first = 'C-G';
var last = 'Lee';

// ES5 : 문자열 연결
console.log('My name is' + first + ' ' + last + '.'); // My name is C-G Lee.
```
- 그러나 `템플릿 리터럴 내`에서는 `표현식 삽입(expression interpolation)이 가능`하다.

```js
var fist = 'C-G';
var lat = 'Lee';

//ES6 : 표현식 삽입
console.log(`My name is ${first} ${last}.`); // My name is C-G Lee.
```

```
🔎 explanation

+ 연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다.
그 외의 경우는 덧셈 연산자로 동작.
```
<br>

# 불리언 타입

> 💡 불리언 타입의 값은 `논리적 참, 거짓`을 나타내는 `true와 false` 뿐이다.

<br>

# undefined 타입

> 💡 undefined 타입의 값은 undefined 가 유일하다.










