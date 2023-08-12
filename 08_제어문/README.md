# 제어문

> 💡 제어문(control flow statement)은 `조건에 따라 코드 블록을 실행(조건문)`하거나 `반복 실행(반복문)`할 때 사용한다.

- 제어문을 사용하면 `코드의 실행 흐름을 인위적으로 제어`할 수 있다.
- 그러나 `코드의 실행 순서가 변경된다는 것`은 단순히 위에서 아래로 순차적으로 진행하는 `직관적인 코드의 흐름을 혼란스럽게` 만든다.

### 블록문

- 블록문(block statement/compund statement)은 `0개 이상의 문을 중괄호로 묶은 것`으로, `코드 블록 또는 블록`이라고 부르기도 한다.

- 문의 끝에는 세미콜론(;)을 붙이는 것이 일반적이지만, `블록문은 자체 종결성`을 갖기 때문에 `세미콜론(;)을 붙이지 않는다.`
<br>

# 조건문

> 💡 조건문(conditional statement)은 주어진 조건식(conditonal expression)의 평가 결과에 따라 코드 블록(블록문)의 실행을 결정한다.
>> `조건식은 불리언 값으로 평가될 수 있는 표현식`이다.
<br>

## if ... else 문

> 💡 if ... else 문은 `논리적 참 또는 거짓에 따라` 실행할 코드 블록을 결정한다.

```js

if (조건식) {
  // 조건식이 참이면 이 코드 블록이 실행된다.
}  else {
  // 조건식이 거짓이면 이 코드 블록이 실행된다.
}

if (조건식1) {
  // 조건식1이 참이면 이 코드 블록이 실행된다.
}  else if (조건식2) {
  // 조건식2가 참이면 이 코드 블록이 실행된다.
}  else {
  // 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
// else if 문과 else문은 옵션으로 사용할 수도 있고 사용하지 않을 수도 있다.
```
- `조건에 따라 단순히 값을 결정`하여 변수에 할당하는 경우 `if ... else 문보다 삼항 조건 연산자를 사용`하는 편이 가독성이 좋다.
  - `조건에 따라 실행할 내용이 복잡`하다면 `if ... else 문을 사용`하자.

## switch 문

> 💡 switch 문은 `주어진 표현식을 평가`하여 그 값과 일치하는 표현식을 갖는 `case 문으로 실행 흐름을 옮긴다.`

```js

switch (표현식) {
  case 표현식1:
    // switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    // switch 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    // switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```
- if ... else 문의 조건식은 불리언 값으로 평가되어야 하지만, switch 문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다.
  - 이는 `if ... else 문은 논리적 참, 거짓`으로 `switch 문은 다양한 상황(case)`에 따라 `실행할 코드 블록을 결정`한다.
- 만약 `if ... else 문으로 해결`할 수 있다면, `switch 문보다 if ... else 문을 사용`하는 편이 좋다.
  - 하지만 `조건식이 너무 많아` switch 문이 더욱 가독성이 좋다면 `switch 문을 사용`하자.
<br>

```
🔎 Note

break문을 사용하지 않을 땐 어떻게 될까?

case 문으로 실행 흐름이 순차적으로 이동하여 문을 실행하지만, 문을 실행한 후 switch 문을 탈출하지 않는다.
switch 문의 모든 case 문을 거치며, 제일 마지막에 있는 case 문 혹은 default 문을 실행하게 된다.

이를 폴스루(fall through)라 한다.

그러나 폴스루를 사용하는 것이 더욱 가독성 좋은 코드로 쓰일 때도 있다.
```

```js

// 폴스루를 사용하여 윤년 계산
var year = 2000; // 2000년은 윤년으로 2월이 29일이다.
var mouth = 2;
var days = 0;

switch (month) {
  case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    days = 31;
    break;
  case 4: case 6: case 9: case 11:
    days = 30;
    break;
  case 2:
    days = ((year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0)) ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}

console.log(days); // 29
```
<br>

# 반복문

> 💡 반복문(loop statement)은 `조건식의 평가 결과가 참`인 경우 `코드 블록을 반복 실행`한다. 이는 조건이 거짓일 때 까지 반복된다.
<br>

## for문

> 💡 for 문은 `조건식이 거짓으로 평가될 때까지` 코드 블록을 반복 실행한다.
>> `for 문`은 `반복 횟수가 명확할 때 사용`한다.

```js

// 일반적으로 사용되는 for 문
for (변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}

// 무한루프 for 문
for(;;) { ... }

// 중첩 for 문
for (;;) {
  for (;;) {
    if () console.log();
  }
}
```

## while 문

> 💡 while 문은 주어진 `조건식의 평가 결과가 참`이면 코드 블록을 계속해서 반복 실행한다.
>> `while 문`은 `반복 횟수가 불명확할 때 사용`한다.

```js

// 일반적으로 사용되는 while 문
var count = 0;

while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}

// 무한루프 while 문
while (true) { ... }
```

## do while 문

> 💡 `do ... while 문`은 `코드 블록을 먼저 실행하고 조건식을 평가`하기 때문에 코드 블록이 무조건 한 번 이상 실행된다.

```js
var count = 0;

do {
  console.log(count); // 0 1 2
  count++;
} while (count < 3);
```
<br>

# break 문

> 💡 `break 문`은 `코드 블록을 탈출`한다.
>> 더 정확히는 레이블 문, 반복문(for, for ... in, for ... of, while, do ... while) 또는 switch 문의 코드 블록을 탈출.

```
🔎 Note

레이블 문(label statement)이란 식별자가 붙은 문을 말한다.

// foo 라는 레이블 식별자가 붙은 레이블 문
foo: console.log('foo');

// foo 라는 식별자가 붙은 레이블 블록문
foo: {
  console.log(1);
  break foo; // foo 레이블 블록문을 탈출한다.
  console.log(2);
}
```

- 그러나 레이블 문은 `중첩된 for 문 외부로 탈출할 때 유용`하지만, `그 밖의 경우`에는 일반적으로 `권장하지 않는다.`
  - `프로그램의 흐름이 복잡`해지며, `가독성이 나빠`지고, `오류를 발생시킬 가능성`이 높아지기 때문.
<br>

# continue 문

> 💡 continue 문은 반복문의 `코드 블록 실행을 현 지점에서 중단`하고, `반복문의 증감식으로 실행 흐름을 이동`시킨다.
>> break 문 처럼 반복문을 탈출하지는 않는다.

- `if 문 내`에서 `실행해야 할 코드가 한 줄이라면,` `continue 문을 사용하지 않는 것`이 가독성이 더 좋다.
  - 하지만 `if 문 내`에서 `실행해야 할 코드가 길다면,` 들여쓰기가 한 단계 더 깊어지므로 `continue 문을 사용하는 편`이 가독성이 더 좋다.

```js

varr string = 'Hello World.';
var search = 'l';
var count = 0;

// continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 한다.
for (var i = 0; i < string.length; i++) {
  // 'l' 이면 카운트를 증가시킨다.
  if (string[i] === search) {
    count++;
    // code
    // code
    // code
  }
}

// continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l' 이 아니면 카운트를 증가시키지 않는다.
  if (string[i] !== search) continue;

  count++;
  // code
  // code
  // code
}
```
