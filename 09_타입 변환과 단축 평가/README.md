# 타입 변환이란?

> 💡 값의 타입은 개발자의 의도에 따라 다른 타입으로 변환할 수 있으며,
`기존 원시 값을 사용`해 `다른 타입의 새로운 원시 값을 생성`하는 것이다.
>> 개발자가 `의도적으로 값의 타입을 변환하는 것`을 `명시적 타입 변환(explicit coercion)` 또는 `타입 캐스팅(type casting)`이라 한다.

>> `자바스크립트 엔진`에 의해 `암묵적으로 타입이 자동 변환`되기도 하며,
이는 `암묵적 타입 변환(implicit coercion`) 또는 타입 `강제 변환(type coercion)` 이라 한다.
<br>

```
🔎 Note

[명시적 타입 변환이나 암묵적 타입 변환이 기존 원시 값을 직접 변경하는 것은 아니다!]

var x = 10;

//명시적 타입 변환
var str = x.toString();
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10


// 암묵적타입 변환
var str = x + '';
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10

이처럼 원시 값은 변경 불가능한 값(immutable value)이므로 변경할 수 없다.
```
<br>

## 1️⃣ 암묵적 타입 변환

> 💡 암묵적 타입 변환이 발생하면 `문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환`한다.
<br>

### 문자열 타입으로 변환

> '+' 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다.
>> 이는 `자바스크립트 엔진이` 피연산자 중에서 `문자열 타입이 아닌 피연산자`를 `문자열 타입으로 암묵적 타입 변환`한다.
<br>

```js

//숫자 타입
0 + ''               // → "0"
-0 + ''              // → "0"
NaN + ''             // → "NaN"
Infinity + ''        // → "Infinity"
-Infinity + ''       // → "Infinity"

// 불리언 타입
true + ''            // → "true"
false + ''           // → "false"

// null 타입
null + ''            // → "null"

// undefined 타입
undefined + ''       // → "undefined"

// 심벌 타입
(Symbol()) + ''      // → TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''            // → "[object Object]"
Math + ''            // → "[object Math]"
[] + ''              // → ""
[10, 20] + ''        // → "10, 20"
(function(){}) + ''  // → "function(){}"
Array + ''           // → "function Array() { [native code] }"

```
<br>

### 숫자 타입으로 변환

> 산술 연산자('-', '*', '/' 등)을 통해,
`산술 연산자의 피연산자` 중에서 `숫자 타입이 아닌 피연산자를` `숫자 타입으로 암묵적 타입 변환`한다.
>> 이때 `피연산자를 숫자 타입으로 변환할 수 없는 경우`는 `산술 연산을 수행할 수 없`으므로 `표현식의 평가 결과는 NaN`이 된다.
<br>

```js

// 문자열 타입
+''               // → 0
+'0'              // → 0
+'1'              // → 1
+ 'string'        // → NaN

// 불리언 타입
+true            // → 1
+false           // → 0

// null 타입
+null            // → 0

// undefined 타입
+undefined       // → NaN

// 심벌 타입
+Symbol()        // → TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}              // → NaN
+[]              // → 0
+[10, 20]        // → NaN
+(function(){})  // → NaN

[주의!]
빈 문자열(''), 빈 배열([]), null false → 0
true → 1
객체와 빈 배열이 아닌 배열, undefined 는 변환되지 않아 → NaN
```
<br>

### 불리언 타입으로 변환

> `자바스크립트 엔진`은 `불리언 타입이 아닌 값`을 `Truthy 값(참으로 평가되는 값) 또는 Falsy 값(거짓으로 평가되는 값)으로 구분`한다.
>> 즉, 제어문의 조건식과 같이 `불리언 값으로 평가되어야 할 문맥`에서
`Truthy 값을 true로, Falsy 값을 false`로 `암묵적 타입 변환`이 된다.
<br>

```js

// 조건식의 평가 결과를 불리언 타입으로 암묵적 변환
if ('')      console.log('1')';
if (true)    console.log('2');
if (0)       console.log('3');
if ('str')   console.log('4');
if (null)    console.log('5');

// 2 4

// false로 평가되는 Falsy 값!
false
undefined
null
0, -0
NaN
''(빈 문자열)

Falsy 값 외의 모든 값을 모두 true로 평가되는 Truthy 값이다.

```
<br>

## 2️⃣ 명시적 타입 변환

> 💡 개발자의 의도에 따라 명시적으로 타입을 변경하는 방법은 다양하다.
>> `표준 빌트인 생성자 함수(String, Number, Boolean)를 연산자 없이 호출`하는 방법

>> `빌트인 메서드`를 사용하는 방법

>> `암묵적 타입 변환`을 이용하는 방법
<br>

### 문자열 타입으로 변환

> `문자열 타입이 아닌 값`을 `문자열 타입으로 변환하는 방법`은 3가지가 있다.
<br>

```js

// 1. String 생성자 함수를 new 연산자 없이 호출
// 숫자 타입 ⇒ 문자열 타입
String(1);                // → "1"
String(NaN);              // → "NaN"
String(Infinity);         // → "Infinity"
// 불리언 타입 ⇒ 문자열 타입
String(true);             // → "true"
String(false);            // → "false"

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 ⇒ 문자열 타입
(1).toString();           // → "1"
(NaN).toString();         // → "NaN"
(Infinity).toString();    // → "Infinity"
// 불리언 타입 ⇒ 문자열 타입
(true).toString();        // → "true"
(false).toString();       // → "false"

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 ⇒ 문자열 타입
1 + '';                   // → "1"
NaN + '';                 // → "NaN"
Infinity + '';            // → "Infinity"
// 불리언 타입 ⇒ 문자열 타입
true + '';                // → "true"
false + '';               // → "false"

```
<br>

### 숫자 타입으로 변환

> `숫자 타입이 아닌 값`을 `숫자 타입으로 변환하는 방법`은 4가지가 있다.
<br>

```js

// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 ⇒ 숫자 타입
Number('0');             // → 0
Number('-1');            // → -1
// 불리언 타입 ⇒ 숫자 타입
Number(true);            // → 1
Number(false);           // → 0

// 2. parseInt, parseFloat 함수를 사용하는 방법([주의!] 문자열만 변환 가능!)
// 문자열 타입 ⇒ 숫자 타입
parseInt('0');           // → 0
parseInt('-1');          // → -1

// 3. + 단항 산술 연산자를 이용하는 방법
// 문자열 타입 ⇒ 숫자 타입
+'0';                    // → 0
// 불리언 타입 ⇒ 숫자 타입
+true;                   // → 1
+false;                  // → 0

// 4. * 산술 연산자를 이용하는 방법
// 문자열 타입 ⇒ 숫자 타입
'0' * 1;                 // → 0
// 불리언 타입 ⇒ 숫자 타입
true * 1;                // → 1
false * 1;               // → 0

```
<br>

### 불리언 타입으로 변환

> `불리언 타입이 아닌 값`을 `불리언 타입으로 변환하는 방법`은 2가지가 있다.
<br>

```js

// 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 ⇒ 불리언 타입
Boolean('x');             // → true
Boolean('');              // → false
Boolean('false');         // → true
// 숫자 타입 ⇒ 불리언 타입
Boolean(1);               // → true
Boolean(NaN);             // → false
Boolean(Infinity);        // → true
// null 타입 ⇒ 불리언 타입
Boolean(null);            // → false
// undefined 타입 ⇒ 불리언 타입
Boolean(undefined);       // → false
// 객체 타입 ⇒ 불리언 타입
Boolean({});              // → true
Boolean([]);              // → true

// 2. ! 부정 논리 연산자를 두 번 사용하는 방법
// 문자열 타입 ⇒ 불리언 타입
!!'x';                    // → true
!!'';                     // → false
!!'false';                // → true
// 숫자 타입 ⇒ 불리언 타입
!!0;                      // → false
!!NaN;                    // → false
!!Infinity;               // → true
// null 타입 ⇒ 불리언 타입
!!null;                   // → false
// undefined 타입 ⇒ 불리언 타입
!!undefined;              // → false
// 객체 타입 ⇒ 불리언 타입
!!{};                     // → true
!![];                     // → true

```
<br>

# 단축 평가

> 💡 단축 평가(short-circuit evaluation)란,
`표현식을 평가하는 도중`에 `평가 결과가 확정된 경우` `나머지 평가 과정을 생략`하는 것을 뜻한다.
>> 논리곱(&&) 연산자와 논리합(||) 연산자는 이처럼 논리 연산의 결과를 결정하는 `피연산자를 타입 변환하지 않고`
`그대로 반환하는 것`을 뜻한다.
<br>

|        단축 평가 표현식         |       평가 결과      |
|---------------------------------|----------------------|
| true ll anything                | true                 |
| false ll anything               | anything             |
| true && anything                | anything             |
| false && anything               | false                |

<br>

## 1️⃣ 논리 연산자를 사용한 단축 평가

> `논리곱(&&) 연산자`는 `두 개의 피연산자가 모두 true로 평가`될 때 `true를 반환`한다.

> `논리합(||) 연산자`는 `두 개의 피연산자 중 하나만 true로 평가`되어도 `true를 반환`한다.
<br>

```js

'Cat' && 'Dog' // → "Dog"

```
- `첫 번째 피연산자 'Cat'은 Truthy 값`이므로 true로 평가하며, `두 번째 피연산자인 'Dog'`가 `논리 연산의 결과를 결정`
  - 따라서 `단축 평가에 의해` `문자열 'Dog'를 그대로 반환`한다.
<br>

```js
'Cat' || 'Dog' // → "Cat"
```
- `첫 번째 피연산자 'Cat'은 Truthy 값`이므로 true로 평가된다. 이 시점에서 `두 번째 피연산자까지 평가할 필요가 없다.`
  - 따라서 `단축 평가에 의해` `문자열 'Cat'을 그대로 반환`한다.
<br>

### 단축 평가의 유용함
<br>

1️⃣ if 문을 대체할 수 있다.

```js

var done = true;
var message = '';

// if 문
if (done) message = '완료';

// if 문은 단축 평가로 대체 가능하다.
message = done && '완료';
console.log(message); // 완료

// if ... else 문
if (done) message = '완료';
else message = '미완료';
console.log(message); // 완료

// if ... else 문은 삼항 조건 연산자로 대체 가능하다.
message = done ? '완료' : '미완료';
console.log(message); // 완료
```
<br>

2️⃣ 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때


```js

// 객체는 키(key)와 값(value)으로 구성된 프로퍼티(property)의 집합이다.
// 만약 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined인 경우
// 객체의 프로퍼티를 참조하면 타입 에러(TypeError)가 발생한다.

var elem = null;
var value = elem.value; // TypeError: Cannot read property 'value' of null

// 이때 단축 평가를 사용하면 에러를 발생시키지 않는다.
// elem이 null 또는 undefined와 같은 Falsy 값이면 elem으로 평가
// elem이 Truthy 값이면 elem.value로 평가
var value = elem && elem.value; // → null

```
<br>

3️⃣ 함수 매개변수에 기본값을 설정할 때

```js

// 함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당된다.
// 이때 단축평가를 사용해 매개변수의 기본값을 설정하면
// undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.

// 단축 평가를 사용한 매개변수의 기본값 설정
function getStringLength(str) {
  str = str || '';
  return str.length;
}

getStringLength();       // → 0
getStringLength('hi');   // → 2

// ES6의 매개변수의 기본값 설정
function getStringLenth(str = '') {
  return str.length;
}

getStringLength();      // → 0
getStringLength('hi');  // → 2
 
```
<br>

## 2️⃣ 옵셔널 체이닝 연산자

> 💡 `옵셔널 체이닝(optional chaining) 연산자 ?.`는 `좌항의 피연산자`가 `null 또는 undefined인 경우 undefined를 반환`하고,
`그렇지 않으면 우항의 프로퍼티 참조`를 이어간다.
>> 이는` 객체를 가리키기를 기대하는 변수`가 `null 또는 undefined가 아닌지 확인`하고 `프로퍼티를 참조할 때 유용`하다.
<br>

```js

//ES11(ECMAScript2020)에서 도입
var elem = null;

// elem이 null 또는 undefined이면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined

```
<br>

### 옵셔널 체이닝 연산자가 도입되기 이전

> `도입되기 이전`에는 `논리 연산자 &&`를 사용한 `단축 평가를 통해 확인`했다.

```js

// elem이 Falsy 값이면 elem으로 평가되고, elem이 Truthy 값이면 elem.value로 평가된다.
var value = elem && elem.value;
console.log(value); // null

```
<br>

> 그러나 `우항의 프로퍼티를 참조하지 못하는 경우`도 있었다.

```js

var str = '';

// 문자열의 길이(length)를 참조한다.
var length = str && str.length;

// 문자열의 길이(length)를 참조하지 못한다.
console.log(length); // ''

```
<br>

## 3️⃣ null 병합 연산자

> 💡 `null 병합(nullish coalescing) 연산자 ??`는 `좌항의 피연산자가 null 또는 undefined인 경우` `우항의 피연산자를 반환`하고,
`그렇지 않으면 좌항의 피연산자를 반환`한다.
>> 이는 `변수에 기본값을 설정할 때 유용`하다.

```js

// E11(ECMAScript2020)에서 도입
var foo = null ?? 'default string';
console.log(foo); // "default string"

```
<br>

### null 병합 연산자가 도입되기 이전

> `도입되기 이전`에는 `논리연산자 ||`를 사용한 `단축 평가를 통해 변수에 기본값을 설정`했다.

> 그러나 평가되는 Falsy 값의 다양성으로 인해 `예기치 않은 동작이 발생할 수도 있다.`

```js

// Falsy 값인 0이나 ''도 기본값으로서 유효하다면 예기지 않은 동작이 발생할 수 있다.
var foo = '' || 'default string';
console.log(foo); // "default string"
```
