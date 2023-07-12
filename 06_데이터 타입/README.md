# 데이터 타입

> 💡 데이터 타입(data type)은 `값의 종류`를 말한다.

- 자바스크립트의 `모든 값은 데이터 타입을 갖는다.`
  - 이때 자바스크립트(ES6)는 `7개의 데이터 타입을 제공`하며,
    이는 `원시 타입(primitive type)과 객체 타입(object/reference type)으로 분류`할 수 있다.
- 자바스크립트는 `객체 기반의 언어`이며, `자바스크립트를 이루고 있는 거의 모든 것이 객체`이다.

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

> 💡 [undefined](https://github.com/CGGGC/ModernJs_deepDive/blob/main/04_%EB%B3%80%EC%88%98/README.md#%EB%B3%80%EC%88%98-%EC%84%A0%EC%96%B8variable-declaration) 타입의 값은 [undefined](https://github.com/CGGGC/ModernJs_deepDive/blob/main/04_%EB%B3%80%EC%88%98/README.md#%EB%B3%80%EC%88%98-%EC%84%A0%EC%96%B8variable-declaration) 가 유일하다.

- undefined는 개발자가 의도적으로 할당하기 위한 값이 아니라, `자바스크립트 엔진`이 `변수를 초기화 할 때 사용하는 값`이다.
  - 변수 참조시 undefined가 반환된다면, 초기화되지 않는 변수
 
```
🔎 explanation

자바스크립트의 undefiend에서 말하는 정의란, 변수에 값을 할당하여 변수의 실체를 명확히 하는 것이다.

C : 선언과 정의는 "실제로 메모리 주소를 할당하는가"로 구분한다.
단순히 컴파일러에게 식별자의 존재만 알리는 것은 선언이고,
실제로 컴파일러가 변수를 생성해서 식별자와 메모리 주소가 연결되면 정의로 구분한다.

JavaScript : 변수를 선언하면 암묵적으로 정의가 이뤄지기 때문에 선언과 정의의 구분이 모호하다.
```
<br>

# null 타입

> 💡 `null은 변수에 값이 없다는 것`을 의도적으로 명시(의도적 부재(intentional absence))할 때 사용하며, `null 타입의 값은 null이 유일`하다.

- `변수에 null을 할당하는 것`은 변수가 `이전에 참조하던 값`을 `더이상 참조하지 않겠다`는 의미이다.
-  또한, `함수가 유효한 값을 반환할 수 없는 경우` 명시적으로 `null을 반환`하기도 한다.

```js
<!DOCTYPE html>
<html>
  <body>
    <script>
      var element = document.querySelector('.myClass');

      // HTML 문서에 myClass 클래스를 갖는 요소가 없다면 null을 반환한다.
      console.log(element); // null
    </script>
  </body>
</html>
```
<br>

# 심벌 타입

> 💡 심벌(symbol)은 `변경 불가능한 원시 타입의 값`이며, `다른 값과 중복되지 않는 유일무이한 값`이다.

- 심벌 이외의 원시 값은 [리터럴](https://github.com/CGGGC/ModernJs_deepDive/tree/main/05_%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC%20%EB%AC%B8#%EB%A6%AC%ED%84%B0%EB%9F%B4)을 통해 생성하지만 `심벌은 Symbol 함수를 호출해 생성`한다.
  - 심벌 값은 외부에 노출되지 않는다.
  - 다른 값과 절대 중복되지 않는 유일무이한 값이다.
 
```js
// 심벌 값 생성
var key = Symbol('key');
console.log(typeof key); / symbol

// 객체 생성
var obj = {};

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); // value
```
<br>

# 데이터 타입의 필요성

- 값을 저장할 때 확보해야 하는 `메모리 공간의 크기를 결정`하기 위해
  - 숫자 값 100을 2진수로 저장할 때, `데이터 타입에 따라 메모리 공간의 할당량이 달라지기 때문`이다.

- 값을 참조할 때 한 번에 읽어 들여야 할 `메모리 공간의 크기를 결정`하기 위해
  - 저장되어 있는 값이 숫자타입일 때, 저장된 메모리 셀의 개수 단위로 읽어들이지 않으면 `값이 훼손되기 때문`이다.
 
- 메모리에서 읽어들인 `2진수를 어떻게 해석할 지 결정`하기 위해서
  - `메모리에 저장된 2진수의 값`을 문자열로 해석할 지 숫자로 해석할 지에 따라 `값이 달라지기 때문`이다.

# 동적 타이핑

> 💡 자바스크립트의 변수는 `선언이 아닌 할당에 의해 타입이 결정(타입 추론(type inference))된다.` 이는 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있음을 뜻한다.
<br>

### 정적 타입(static/strong type) 언어
<br>

- `변수를 선언할 때` 변수에 할당할 수 있는 값의 종류, 즉 `데이터 타입을 사전에 선언`해야한다.
  - ex) C, C++, Java, Kotlin 등

```c
// c 변수에는 1바이트 정수 타입의 값(-128~127)만 할당할 수 있다.
char c;

// num 변수에는 4바이트 정수 타입의 값(-2,124,483,643 ~ 2,124,483,643)만 할당할 수 있다.
int num;
```

- `정적 타입의 언어`는 `변수의 타입을 변경할 수 없으며,` `변수에 선언한 타입에 맞는 값만 할당`할 수 있다.
- `컴파일 시점`에서 `타입 체크(선언한 데이터 타입에 맞는 값을 할당했는지 검사하는 처리)를 수행`한다.
<br>

### 동적 타입(dynamic/weak type) 언어
<br>

- `변수를 선언할 때 타입을 선언하지 않으며,` var, let, const 키워드를 사용해 변수를 선언한다.
  - ex) JavaScript, Python, PHP, Ruby 등

```js
var foo;
console.log(typeof foo); // undefined

foo = 3;
console.log(typeof foo); //number

foo = 'Hello';
console.log(typeof foo); //string

foo = {};
console.log(typeof foo); //object

foo = function() {};
console.log(typeof foo); // function
```

- typeof 연산자로 `변수에 할당된 값`의 `데이터 타입을 반환`한다.
  - 변수의 데이터 타입을 반환하는 것이 아니다.
- `값을 할당하는 시점`에 `변수의 타입이 동적으로 결정`된다.
<br>

```
🔎 explanation

자바스크립트의 모든 값은 데이터 타입을 갖는다고 했다. 그렇다면 변수는 데이터 타입을 가질까?

기본적으로 변수는 타입을 갖지 않는다. 하지만 값은 타입을 갖는다.
따라서 현재 변수에 할당되어 있는 값에 의해 변수의 타입이 동적으로 결정된다고 표현하는 것이 더 적절하다.
```

### 동적 타입 언어의 단점
<br>

> 💡 동적 타입 언어는 `유연성(flexibility)은 높지만` `신뢰성(reliability)은 떨어진다.`

- 변수 값은 언제든지 변경될 수 있으므로, `변화하는 변수 값을 추적하기 어려울 수도 있다.`

- 변수의 타입이 고정되어 있지 않기 때문에, 변수는 값의 변경에 의해 타입이 언제든지 변경될 수 있다.
  - 이는, `값을 확인하지 전 까지 변수의 데이터 타입을 확신할 수 없다.`

- `개발자의 의도와는 상관없이` 암묵적으로 `타입이 자동으로 변환될 수 있다.`
  - 즉, 숫자 타입의 변수일 것이라고 예측했지만, 문자열이 될 수도 있다는 말이다.


```
🔎 explanation

자바스크립트에서 변수 사용시 주의사항

1️⃣ 변수는 꼭 필요한 경우에 한해 제한적으로 사용하자.
   무분별한 변수의 사용은 예측을 어렵게 만들어 오류를 야기한다.

2️⃣ 변수의 유효 범위(스코프)는 최대한 좁게 만들어 변수의 부작용을 억제하자.

3️⃣ 전역 변수는 최대한 사용하지 않도록 하자.
   어디서든지 참조/변경이 가능하기 때문에 의도치 않게 값이 변경될 수도, 다른 코드에 영향을 줄 수도 있다.

4️⃣ 변수보다는 상수를 사용해 값의 변경을 억제하자.

5️⃣ 변수 이름은 변수의 목적이나 의미를 파악할 수 있도록 네이밍하자.
   명확한 네이밍은 코드를 이해하기 쉽게 만들어주고, 협업과 생산성 향상에 도움을 준다.
```

> ⭐ 가독성이 좋은 코드가 좋은 코드다.






