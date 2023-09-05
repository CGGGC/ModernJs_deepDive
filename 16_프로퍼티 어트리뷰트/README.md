# 내부 슬롯과 내부 메서드

> 💡 `내부 슬롯(internal slot) & 내부 메서드(internal method)` : JS엔진의 내부 로직
>> 구현 알고리즘을 설명하기 위해 ES 사양에서 사용하는 의사 프로퍼티(pseudo property) & 의사 메서드(pseudo method)
<br>

- 원칙적으로 JS는 내부 슬롯과 내부 메서드에 **직접적으로 접근하거나 호출할 수 있는 방법을 제공 X**
+ 단, **일부 내부 슬롯 & 내부 메서드에 한해 간접 접근 수단을 제공**한다.
  + 예를들어, [[PPrototype]] 내부 슬롯은 __proto__를 통해 간접 접근을 허용한다.

```js

const o = {};

// [[Prototype]]
// 내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없다.
o.[[Prototype]] // → "Uncaught SyntaxError: Unexpected token '['

// __proto__
// 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공하기는 한다.
o.__proto__ // → Object.prototype

```
<br>

# 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

> 💡 `프로퍼티 어트리뷰트` : JS엔진은 프로퍼티를 생성할 때 `프로퍼티의 상태`를 기본값으로 자동 정의
>> 프로퍼티 상태 : `프로퍼티의 값(value)`, `값의 갱신 가능 여부(writable)`,
`열거 가능 여부(enumberable)`, `재정의 가능 여부(configurable)`
<br>

- 프로퍼티 어트리뷰트는 내부 상태 값(meta-property)인 **내부 슬롯**이다.
  - **[[Writable]], [[Enumerable]], [[Configurable]]**

+ 따라서 프로퍼티 어트리뷰트에 **직접 접근 X, 간접적으로만 확인**할 수 있다.
  + **Object.getOwnPropertyDescriptor 메서드**를 사용!

```js

const person = {
  name: 'Lee'
};

// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다.
// 첫 매개변수에는 객체의 참조, 두번째 매개변수에는 프로퍼티 키를 문자열로 전달
console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: "Lee", writable: true, enumerable: true, configurable: true}

```
<br>

> 💡 `프로퍼티 디스크립터(PropertyDescriptor)` : 프로퍼티 어트리뷰트 정보를 제공하는 객체
<br>

- **존재하지 않는 프로퍼티나 상속받은 프로퍼티**에 대한 프로퍼티 디스크립터를 요구하면 **undefiend가 반환**된다.

+ **Object.getOwnpropertyDescriptors 메서드**를 사용!
  + 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환

```js

const person = {
  name: 'Lee'
};

// 프로퍼티 동적 생성
person.age = 20;

// 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.
// 매개변수에는 오로지 객체의 참조만 전달
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
  name: {value: "Lee", writable: true, enumerable: true, configurable: true},
  age: {value: 20, writable: true, enumerableL true, configuableL true}
}
*/

```
<br>

# 프로퍼티의 구분

## 1️⃣ 데이터 프로퍼티

> 💡 `데이터 프로퍼티(data property)` : 키와 값으로 구성된 일반적인 프로퍼티
>> 지금까지 살펴본 모든 프로퍼티는 데이터 프로퍼티다.
<br>

|  프로퍼티 어트리뷰트    |  프로퍼티 디스크립트 객체의 프로퍼티  |  설명                                          |
|------------------------|---------------------------------------|------------------------------------------------|
| [[Value]]              | value                                 | 프로퍼티 키를 통해 프로퍼티 값에 접근시, 반환되는 값|
| [[Writable]]           | writable                              | 프로퍼티 값의 변경 가능 여부를 명시, 불리언 값 |
| [[Enumerable]]         | enumerable                            | 프로퍼티의 열거 가능 여부를 명시, 불리언 값    |
| [[Configurable]]       | configurable                          | 프로퍼티의 재정의 가능 여부를 명시, 불리언 값  |
<br>

```js

const person = {
  name: "Lee"
};

// 프로퍼티 동적 생성
person.age = 20;

console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: "Lee", writable: true, enumerable: true, configurable: true}

console.log(Object.getOwnPropertyDescriptors(person));
/*
{
  name: {value: "Lee", writable: true, enumerable: true, configurable: true},
  age: {value: 20, writable: true, enumerable: true, configurable: true}
}
*/
```

- 프로퍼티가 생성될 때 `[[Value]]의 값`은 `프로퍼티 값`으로 초기화된다.
- `[[Writable]], [[Enumerable]], [[Configurable]]의 값`은 `true`로 초기화된다.

+ 프로퍼티를 `동적 추가`해도 마찬가지로 값이 초기화된다.
<br>

## 2️⃣ 접근자 프로퍼티

> 💡 `접근자 프로퍼티(accessor property)` : 자체적으로 값을 가지지 않는 프로퍼티
>> 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 `접근자 함수(accessor function)로 구성`
<br>

|  프로퍼티 어트리뷰트    |  프로퍼티 디스크립트 객체의 프로퍼티  |  설명                                                  |
|------------------------|---------------------------------------|--------------------------------------------------------|
| [[Get]]                | get                                   | 프로퍼티 값을 읽을시, getter 함수 호출 & 결과가 값으로 반환|
| [[Set]]                | set                                   | 프로퍼티 값을 저장시, setter 함수 호출 & 결과가 값으로 저장|
| [[Enumerable]]         | enumerable                            | 데이터 프로퍼티의 [[Enumerable]]과 같다.                 |
| [[Configurable]]       | configurable                          | 데이터 프로퍼티의 [[Configurabe]]과 같다.                |
<br>

- `접근자 함수`는 `getter / setter 함수`라고도 부른다.
  - `getter 와 setter 함수`를 모두 정의하거나, 또는 하나만 정의할 수도 있다.
<br>

```js

const person = {
  // 데이터 프로퍼티
  firstName: 'CG',
  lastName: 'Lee',

  // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수
  set fullName(name) {
    [this.fistName, this.lastName] = name.split(' ');
  }
};


// 데이터 프로퍼티를 통한 프로퍼티 값의 참조
  console.log(person.firstName + ' ' + person.lastName); // CG Lee

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = 'CCCCGGGG Lee';
console.log(person); // {firstName: "CCCCGGGG", lastName: "Lee"}

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // CCCCGGGG Lee


// 데이터 프로퍼티인 fistName
// [[Value]], [[Writable]], [[Enumerable]], [[Configurable]] 프로퍼티 어트리뷰트를 갖는다.
let descriptor = Object.getOwnPropertyDescriptor(person, 'fistName');
console.log(descriptor);
// {value: "CCCCGGGG", writable: true, enumerable: true, configurable: true}

// fullName은 접근자 프로퍼티
// [[Get]], [[Set]], [[Enumerable]], [[Configurable]] 프로퍼티 어트리뷰트를 갖는다
descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log(descriptor);
// {get: f, set: f, enumerable: true, configurable: true}

```

```js
🔎 Note

[접근자 & 데이터 프로퍼티 구별 방법]

Object.getOwnPropertyDescriptor(Object.prototype, '__proto__');
// {get: f, se: f, enumerable: false, configurable: true}

Object.getOwnPropertyDescriptor(function() {}, 'prototype');
// {value: { ... }, writable: true, enumerable: false, configurable: flase}

→ "일반 객체"의 __proto__ 는 접근자 프로퍼티

→ "함수 객체"의 prototype은 데이터 프로퍼티
```
<br>

# 프로퍼티 정의

> 💡 `프로퍼티 정의` : `새로운 프로퍼티를 추가하면서` 프로퍼티 어트리뷰트를 `명시적으로 정의` & 기존 프로퍼티의 프로퍼티 어트리뷰트를 `재정의`
>> ex) 프로퍼티 값을 갱신 가능하도록 할 지 정의
<br>

```js

const person = {};

// 데이터 프로퍼티 정의
Object.defineProperty(person, 'fristName', {
  value: 'CG',
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(person, 'lastName', {
  value: 'Lee'
});

let descriptor = Object.getOwnPropertyDescriptor(person, 'fistName');
console.log('firstName', descriptor);
// fristName {value: "CG", writable: true, enumerable: true, configurable: true}

// 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName {value: "Lee", writable: false, enumerable: false, configurable: false}

[기본 값이 false 일 때]

- [[Enmerable]]의 값이 false인 경우
  해당 프로퍼티는 for ... in 문이나 Object.keys 등으로 열거할 수 없다.

- [[Writable]]의 값이 false 인 경우
  해당 프로퍼티는 [[Value]]의 값을 변경할 수 없다.

- [[Configurable]]의 값이 false 인 경우
  해당 프로퍼티를 삭제할 수 없으며 재정의할 수 없다.
  또한, 프로퍼티를 삭제하면 에러는 발생하지 않고 무시된다.


// 접근자 프로퍼티 정의
Obejct.definedProperty(person, 'fullName', {
  // getter 함수
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수
  set(name) {
    [this.firstName, this.lastName] = name.split(' ');
  },
  enumerable: true,
  configurable: true
});

descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log('fullName', descriptor);
// fullName {get: f, set: f, enumerable: true, configurable: true}

person.fullName = 'CG Lee';
console.log(person); // {firstName: "CG", lastName: "Lee"}


[Object.definedPropertyies 메서드 사용시 여려 개의 프로퍼티를 한 번에 정의 가능!]

Object.definedProperties(person, {
  // 데이터 프로퍼티 정의
  firstName: {
    value: '...',
    writable: true
    ...
  },
  lastName: {
    ...
  },
  // 접근자 프로퍼티 정의
  fullName: {
    // getter 함수
    get () {
      return ...
    },
    // setter 함수
    set(name) {
      [this....
    },
    enumerable: true,
    configurable: true
  }
});

```
<br>

|  프로퍼티 디스크립터 객체의 프로퍼티   |  대응하는 프로퍼티 어트리뷰트  |  생략했을 때의 기본값                |
|----------------------------------------|-------------------------------|--------------------------------------|
| value                                  | [[Value]]                     | undefined                            |
| get                                    | [[Get]]                       | undefined                            |
| set                                    | [[Set]]                       | undefined                            |
| writable                               | [[Writable]]                  | false                                |
| enumerable                             | [[Enumerable]]                | false                                |
| configurable                           | [[Configurable]]              | false                                |
<br>

# 객체 변경 방지

```js
🔎 Note

객체는 변경 가능한 값! → 재할당 없이 직접 변경할 수 있다.

"프로퍼티를 추가 & 삭제", "프로퍼티 값 갱신",
Object.definedProperty 메서드를 사용하여 "프로퍼티 어트리뷰트를 재정의" 가능!

따라서, 객체의 변경을 방지하는 다양한 메서드를 제공한다.
이 메서드들은 객체의 변경을 "금지하는 강도"가 다르다.
```
<br>

|  구분          |  메서드                  | 프로퍼티 추가 | 프로퍼티 삭제 | 프로퍼티 값 읽기 | 프로퍼티 값 쓰기 | 프로퍼티 어트리 뷰트 재정의 |
|----------------|--------------------------|--------------|---------------|------------------|------------------|-----------------------------|
|객체 확장 금지   | Object.preventExtensions | X            | O             | O                | O                | O                           |
|객체 밀봉       | Object.seal              | X             | X             | O                | O                | X                           |
|객체 동결       | Object.freeze            | X             | X             | O                | X                | X                           |
<br>

## 1️⃣ 객체 확장 금지

> 확장이 금지된 객체는 `프로퍼티 추가가 금지`된다.
>> 프로퍼티 동적 추가 & Object.defineProperty 메서드 추가 전부 금지
<br>

## 2️⃣ 객체 밀봉

> 밀봉된 객체는 `읽기와 쓰기만 가능`하다.
>> 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지
<br>

## 3️⃣ 객체 동결

> 동결된 객체는 `읽기만 가능`하다.
>> 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지
<br>

## 불변 객체
