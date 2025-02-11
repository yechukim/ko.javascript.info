# while과 for 반복문

개발을 하다 보면 여러 동작을 반복해야 하는 경우가 종종 생깁니다.

상품 목록에서 상품을 차례대로 출력하거나 숫자를 1부터 10까지 하나씩 증가시키면서 동일한 코드를 반복 실행해야 하는 경우같이 말이죠.

*반복문(loop)* 을 사용하면 동일한 코드를 여러 번 반복할 수 있습니다.

## 'while' 반복문

`while` 반복문의 문법은 다음과 같습니다.

```js
while (condition) {
  // 코드
  // '반복문 본문(body)'이라 불림
}
```

`condition`(조건)이 truthy 이면 반복문 본문의 `코드`가 실행됩니다.

아래 반복문은 조건 `i < 3`을 만족할 동안 `i`를 출력해줍니다.

```js run
let i = 0;
while (i < 3) { // 0, 1, 2가 출력됩니다.
  alert( i );
  i++;
}
```

반복문 본문이 한 번 실행되는 것을 *반복(iteration, 이터레이션)* 이라고 부릅니다. 위 예시에선 반복문이 세 번의 이터레이션을 만듭니다.

`i++`가 없었다면 이론적으로 반복문이 영원히 반복되었을 겁니다. 그런데 브라우저는 이런 무한 반복을 멈추게 해주는 실질적인 수단을 제공합니다. 서버 사이드 자바스크립트도 이런 수단을 제공해 주므로 무한으로 반복되는 프로세스를 종료할 수 있습니다.

반복문 조건엔 비교뿐만 아니라 모든 종류의 표현식, 변수가 올 수 있습니다. 조건은 `while`에 의해 평가되고, 평가 후엔 불린값으로 변경됩니다.

아래 예시에선 `while (i != 0)`을 짧게 줄여 `while (i)`로 만들어보았습니다.

```js run
let i = 3;
*!*
while (i) { // i가 0이 되면 조건이 falsy가 되므로 반복문이 멈춥니다.
*/!*
  alert( i );
  i--;
}
```

````smart header="본문이 한 줄이면 대괄호를 쓰지 않아도 됩니다."
반복문 본문이 한 줄짜리 문이라면 대괄호 `{…}`를 생략할 수 있습니다.

```js run
let i = 3;
*!*
while (i) alert(i--);
*/!*
```
````

## 'do..while' 반복문

`do..while` 문법을 사용하면 `condition`을 반복문 본문 *아래*로 옮길 수 있습니다.

```js
do {
  // 반복문 본문
} while (condition);
```

이때 본문이 먼저 실행되고, 조건을 확인한 후 조건이 truthy인 동안엔 본문이 계속 실행됩니다.

예시:

```js run
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```

`do..while` 문법은 조건이 truthy 인지 아닌지에 상관없이, 본문을 **최소한 한번**이라도 실행하고 싶을 때만 사용해야 합니다. 대다수의 상황에선 `do..while`보다 `while(…) {…}`이 적합합니다.

## 'for' 반복문

`for` 반복문은 `while` 반복문보다는 복잡하지만 가장 많이 쓰이는 반복문입니다.

문법은 다음과 같습니다.

```js
for (begin; condition; step) {
  // ... 반복문 본문 ...
}
```

`for`문을 구성하는 각 요소가 무엇을 의미하는지 알아봅시다. 아래 반복문을 실행하면  `i`가 `0`부터 `3`이 될 때까지(단, `3`은 포함하지 않음) `alert(i)`가 호출됩니다.

```js run
for (let i = 0; i < 3; i++) { // 0, 1, 2가 출력됩니다.
  alert(i);
}
```

이제 `for`문의 구성 요소를 하나씩 살펴봅시다.

| 구성 요소  |          |                                                                            |
|-------|----------|----------------------------------------------------------------------------|
| begin | `i = 0`    | 반복문에 진입할 때 단 한 번 실행됩니다.                                      |
| condition | `i < 3`| 반복마다 해당 조건이 확인됩니다. false이면 반복문을 멈춥니다.              |
| body | `alert(i)`| condition이 truthy일 동안 계속해서 실행됩니다.                         |
| step| `i++`      | 각 반복의 body가 실행된 이후에 실행됩니다. |

일반적인 반복문 알고리즘은 다음과 같습니다.

```
begin을 실행함
→ (condition이 truthy이면 → body를 실행한 후, step을 실행함)
→ (condition이 truthy이면 → body를 실행한 후, step을 실행함)
→ (condition이 truthy이면 → body를 실행한 후, step을 실행함)
→ ...
```

`begin`이 한 차례 실행된 이후에, `condition` 확인과 `body`, `step`이 계속해서 반복 실행되죠.

반복문을 처음 배우신다면, 위 예시를 실행했을 때 어떤 과정을 거쳐 얼럿 창이 출력되는지 종이에 적어가며 공부해보세요. 이렇게 하면 반복문을 쉽게 이해할 수 있습니다.

정확히 어떤 과정을 거치는지는 아래 예시에서 확인할 수 있습니다.

```js
// for (let i = 0; i < 3; i++) alert(i)

// begin을 실행함
let i = 0
// condition이 truthy이면 → body를 실행한 후, step을 실행함
if (i < 3) { alert(i); i++ }
// condition이 truthy이면 → body를 실행한 후, step을 실행함
if (i < 3) { alert(i); i++ }
// condition이 truthy이면 → body를 실행한 후, step을 실행함
if (i < 3) { alert(i); i++ }
// i == 3이므로 반복문 종료
```

````smart header="인라인 변수 선언"
지금까진 '카운터' 변수 `i`를 반복문 안에서 선언하였습니다. 이런 방식을 '인라인' 변수 선언이라고 부릅니다. 이렇게 선언한 변수는 반복문 안에서만 접근할 수 있습니다.

```js run
for (*!*let*/!* i = 0; i < 3; i++) {
  alert(i); // 0, 1, 2
}
alert(i); // Error: i is not defined
```

인라인 변수 선언 대신, 정의되어있는 변수를 사용할 수도 있습니다.

```js run
let i = 0;

for (i = 0; i < 3; i++) { // 기존에 정의된 변수 사용
  alert(i); // 0, 1, 2
}

alert(i); // 3, 반복문 밖에서 선언한 변수이므로 사용할 수 있음
```

````


### 구성 요소 생략하기

`for`문의 구성 요소를 생략하는 것도 가능합니다.

반복문이 시작될 때 아무것도 할 필요가 없으면 `begin`을 생략하는 것이 가능하죠.

예시를 살펴봅시다.

```js run
let i = 0; // i를 선언하고 값도 할당하였습니다.

for (; i < 3; i++) { // 'begin'이 필요하지 않기 때문에 생략하였습니다.
  alert( i ); // 0, 1, 2
}
```

`step` 역시 생략할 수 있습니다.

```js run
let i = 0;

for (; i < 3;) {
  alert( i++ );
}
```

위와 같이 `for`문을 구성하면 `while (i < 3)`과 동일해집니다.

모든 구성 요소를 생략할 수도 있는데, 이렇게 되면 무한 반복문이 만들어집니다.

```js
for (;;) {
  // 끊임 없이 본문이 실행됩니다.
}
```

`for`문의 구성요소를 생략할 때 주의할 점은 두 개의 `;` 세미콜론을 꼭 넣어주어야 한다는 점입니다. 하나라도 없으면 문법 에러가 발생합니다.

## 반복문 빠져나오기

대개는 반복문의 조건이 falsy가 되면 반복문이 종료됩니다.

그런데 특별한 지시자인 `break`를 사용하면 언제든 원하는 때에 반복문을 빠져나올 수 있습니다.

아래 예시의 반복문은 사용자에게 일련의 숫자를 입력하도록 안내하고, 사용자가 아무런 값도 입력하지 않으면 반복문을 '종료'합니다.

```js run
let sum = 0;

while (true) {

  let value = +prompt("숫자를 입력하세요.", '');

*!*
  if (!value) break; // (*)
*/!*

  sum += value;

}
alert( '합계: ' + sum );
```

`(*)`로 표시한 줄에 있는 `break`는 사용자가 아무것도 입력하지 않거나 `Cancel`버튼을 눌렀을 때 활성화됩니다. 이때 반복문이 즉시 중단되고 제어 흐름이 반복문 아래 첫 번째 줄로 이동합니다. 여기선 `alert`가 그 첫 번째 줄이 되겠죠.

반복문의 시작 지점이나 끝 지점에서 조건을 확인하는 것이 아니라 본문 가운데 혹은 본문 여러 곳에서 조건을 확인해야 하는 경우, '무한 반복문 + `break`' 조합을 사용하면 좋습니다.

## 다음 반복으로 넘어가기 [#continue]

`continue` 지시자는 `break`의 '가벼운 버전'입니다. `continue`는 전체 반복문을 멈추지 않습니다. 대신에 현재 실행 중인 이터레이션을 멈추고 반복문이 다음 이터레이션을 강제로 실행시키도록 합니다(조건을 통과할 때).

`continue`는 현재 반복을 종료시키고 다음 반복으로 넘어가고 싶을 때 사용할 수 있습니다.

아래 반복문은 `continue`를 사용해 홀수만 출력합니다.

```js run no-beautify
for (let i = 0; i < 10; i++) {

  // 조건이 참이라면 남아있는 본문은 실행되지 않습니다.
  *!*if (i % 2 == 0) continue;*/!*

  alert(i); // 1, 3, 5, 7, 9가 차례대로 출력됨
}
```

`i`가 짝수이면 `continue`가 본문 실행을 중단시키고 다음 이터레이션이 실행되게 합니다(`i`가 하나 증가하고, 다음 반복이 실행됨). 따라서 `alert` 함수는 인수가 홀수일 때만 호출됩니다.

````smart header="`continue`는 중첩을 줄이는 데 도움을 줍니다."
홀수를 출력해주는 예시는 아래처럼 생길 수도 있습니다.

```js run
for (let i = 0; i < 10; i++) {

  if (i % 2) {
    alert( i );
  }

}
```

기술적인 관점에서 봤을 때, 이 예시는 위쪽에 있는 예시와 동일합니다. `continue`를 사용하는 대신 코드를 `if` 블록으로 감싼 점만 다릅니다.

그런데 이렇게 코드를 작성하면 부작용으로 중첩 레벨(대괄호 안의 `alert` 호출)이 하나 더 늘어납니다. `if` 안의 코드가 길어진다면 전체 가독성이 떨어질 수 있습니다.
````

````warn header="'?' 오른쪽엔 `break`나 `continue`가 올 수 없습니다."
표현식이 아닌 문법 구조(syntax construct)는 삼항 연산자 `?`에 사용할 수 없다는 점을 항상 유의하시기 바랍니다. 특히 `break`나 `continue` 같은 지시자는 삼항 연산자에 사용하면 안 됩니다.

아래와 같은 조건문이 있다고 해봅시다.

```js
if (i > 5) {
  alert(i);
} else {
  continue;
}
```

물음표를 사용해서 위 조건문을 아래와 같이 바꾸려는 시도를 할 수 있을겁니다.


```js no-beautify
(i > 5) ? alert(i) : *!*continue*/!*; // 여기에 continue를 사용하면 안 됩니다.
```

이런 코드는 문법 에러를 발생시킵니다.

이는 물음표 연산자 `?`를 `if`문 대용으로 쓰지 말아야 하는 이유 중 하나입니다.
````

## break/continue와 레이블

여러 개의 중첩 반복문을 한 번에 빠져나와야 하는 경우가 종종 생기곤 합니다.

`i`와 `j`를 반복하면서 프롬프트 창에 `(0,0)`부터 `(2,2)`까지를 구성하는 좌표 `(i, j)`를 입력하게 해주는 예시를 살펴봅시다.

```js run no-beautify
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`(${i},${j})의 값`, '');

    // 여기서 멈춰서 아래쪽의 `완료!`가 출력되게 하려면 어떻게 해야 할까요?
  }
}

alert('완료!');
```

사용자가 `Cancel` 버튼을 눌렀을 때 반복문을 중단시킬 방법이 필요합니다.

`input` 아래에 평범한 `break` 지시자를 사용하면 안쪽에 있는 반복문만 빠져나올 수 있습니다. 이것만으론 충분하지 않습니다(중첩 반복문을 포함한 반복문 두 개 모두를 빠져나와야 하기 때문이죠 - 옮긴이). 이럴 때 레이블을 사용할 수 있습니다.

*레이블(label)* 은 반복문 앞에 콜론과 함께 쓰이는 식별자입니다.
```js
labelName: for (...) {
  ...
}
```

반복문 안에서 `break <labelName>`문을 사용하면 레이블에 해당하는 반복문을 빠져나올 수 있습니다.

```js run no-beautify
*!*outer:*/!* for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`(${i},${j})의 값`, '');

    // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나옵니다.
    if (!input) *!*break outer*/!*; // (*)

    // 입력받은 값을 가지고 무언가를 함
  }
}
alert('완료!');
```

위 예시에서 `break outer`는 `outer`라는 레이블이 붙은 반복문을 찾고, 해당 반복문을 빠져나오게 해줍니다.

따라서 제어 흐름이 `(*)`에서 `alert('완료!')`로 바로 바뀝니다.

레이블을 별도의 줄에 써주는 것도 가능합니다.

```js no-beautify
outer:
for (let i = 0; i < 3; i++) { ... }
```

`continue` 지시자를 레이블과 함께 사용하는 것도 가능합니다. 두 가지를 같이 사용하면 레이블이 붙은 반복문의 다음 이터레이션이 실행됩니다.

````warn header="레이블은 마음대로 '점프'할 수 있게 해주지 않습니다."
레이블을 사용한다고 해서 원하는 곳으로 마음대로 점프할 수 있는 것은 아닙니다.

아래 예시처럼 레이블을 사용하는 것은 불가능합니다.
```js
break label; // 아래 for 문으로 점프할 수 없습니다.

label: for (...)
```

`break`와 `continue`는 반복문 안에서만 사용할 수 있고, 레이블은 반드시 `break`이나 `continue` 지시자 위에 있어야 합니다.
````

## 요약

지금까지 세 종류의 반복문에 대해 살펴보았습니다.

- `while` -- 각 반복이 시작하기 전에 조건을 확인합니다.
- `do..while` -- 각 반복이 끝난 후에 조건을 확인합니다.
- `for (;;)` -- 각 반복이 시작하기 전에 조건을 확인합니다. 추가 세팅을 할 수 있습니다.

'무한' 반복문은 보통 `while(true)`를 써서 만듭니다. 무한 반복문은 여타 반복문과 마찬가지로 `break` 지시자를 사용해 멈출 수 있습니다.

현재 실행 중인 반복에서 더는 무언가를 하지 않고 다음 반복으로 넘어가고 싶다면 `continue` 지시자를 사용할 수 있습니다.

반복문 앞에 레이블을 붙이고, `break/continue`에 이 레이블을 함께 사용할 수 있습니다. 레이블은 중첩 반복문을 빠져나와 바깥의 반복문으로 갈 수 있게 해주는 유일한 방법입니다.
