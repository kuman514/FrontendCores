# JavaScript

## 원시값
- 문자열 (string)
- 숫자 (number)
- 불리언 (boolean)
- null
- undefined
- BigInt
- 심볼 (Symbol)

## var, let, const
- var
  - 함수 레벨(함수 내에서 선언되었을 경우) 또는 전역 스코프 변수.
  - 재선언 가능. (같은 식별자로 var 중복 선언 가능)
  - 재할당 가능. (= 연산자를 통한 값 갱신 가능)
  - 호이스팅 가능. (선언부 위에서 참조 가능)
- let
  - 블록 레벨 스코프 변수. 블록(중괄호({})로 감싸인 범위)을 벗어나면 참조할 수 없다.
  - 재선언 불가. (같은 식별자로 let 중복 선언 불가)
  - 재할당 가능. (= 연산자를 통한 값 갱신 가능)
  - 호이스팅 불가. (선언부 위에서 참조 불가)
- const
  - 블록 레벨 스코프 변수. 블록(중괄호({})로 감싸인 범위)을 벗어나면 참조할 수 없다.
  - 재선언 불가. (같은 식별자로 const 중복 선언 불가)
  - 재할당 불가. (= 연산자를 통한 값 갱신 불가)
  - 호이스팅 불가. (선언부 위에서 참조 불가)

## null, undefined, 선언되지 않은 변수
- null
  - 명시적으로 비어있다고 표현된 값.
  - falsy한 값이기 때문에, 명시적으로 null임을 확인하고자 한다면 === 연산자를 사용하자.
- undefined
  - 선언되었으나 아직 할당되지 않았을 때의 값.
  - 함수가 값을 리턴하지 않을 때에도 undefined가 나온다.
  - falsy한 값이기 때문에, 명시적으로 undefined임을 확인하고자 한다면 === 연산자를 사용하자.
- 선언되지 않은 변수
  - var, let, const를 사용하여 선언되지 않은 변수.
  - `'use strict'`를 통해 Strict 모드가 되었을 때 사용 시 Reference Error가 발생하며, 아닐 경우 전역에 자동으로 추가된다.

## 이벤트 루프
- 이벤트 루프란
  - JavaScript에서 동작하는 싱글 스레드 루프.
- 틱 (Tick) 작동 과정
  - 콜 스택이 비어있는지 확인한다.
  - 태스크 큐에 실행할 작업을 확인한다.
  - 콜 스택이 비어있고 태스크 큐에 대기 중인 콜백이 있으면, 해당 콜백을 큐에서 빼내에 실행을 위해 콜 스택에 추가된다.
  - 해당 반복적인 작업을 하나의 틱이라고 부른다.
- 메모리 힙
  - 객체들이 저장되는 영역.
- 콜 스택
  - 코드가 실행될 때 쌓이기 시작하는 영역. 코드가 실행될 때 스택 형태로 쌓인다.
  - 지역 변수나 파라미터는 콜 스택 밖에서 저장된다. JavaScript에서 클로저가 가능한 이유이기도 하다.
- 태스크 큐
  - 비동기적으로 실행되는 함수들이 보관되는 영역이다.
  - Web API, setTimeout, 외부 통신 등 비용이 높은 작업에 대한 콜백을 대기시키는 큐.
  - JavaScript 엔진 외에 있다.
  - 마이크로태스크 큐? 매크로태스크 큐?

## 프로토타입
- 객체의 \_\_proto\_\_ 속성.
- 모든 JavaScript 객체는 프로토타입을 가지고 있으며, 이는 객체의 원형이다.
- 객체 자체에 찾고자 하는 멤버가 없으면 \_\_proto\_\_의 멤버를 찾으며, 거기서도 멤버가 없으면 계속해서 \_\_proto\_\_를 거듭하며 찾는다.
- 모든 객체는 공통 조상에 다다를 때까지 \_\_proto\_\_ 속성을 참조하며, 공통 조상의 \_\_proto\_\_는 null이다.

## 이벤트 버블링
- 어떤 엘리먼트에서 클릭이나 변경 등의 이벤트가 발생하였을 때, 해당 엘리먼트부터 시작해서 최상단 엘리먼트에 도달할 때까지 이벤트가 부모 엘리먼트로 전파되는 현상.
- 이를 멈추려면 (이벤트 객체).stopPropagation()을 호출한다.

## 이벤트 위임
- 이벤트 버블링의 특성을 활용하여, 자식 엘리먼트의 이벤트 핸들링을 부모 엘리먼트에 이관하는 방법을 말한다.
- 이벤트를 핸들링 해야할 자식 엘리먼트가 여러 개 있고 그 여러 핸들링이 서로 비슷할 때, 부모 엘리먼트에 이관하는 것이 이벤트 핸들링의 유지보수를 더욱 용이하게 할 수 있다.

## Function 객체
- Function()
- new Function()

## this가 정해지는 우선순위
1. new 객체 생성을 통해 생성되었는가?
2. .call, .bind, .apply의 thisArg 파라미터로 전달받았는가?
3. 객체의 멤버로써 존재하는가?
4. 일반적인 호출인가?
- 1번 ~ 4번 조건 중 여러 개를 충족한다면, 1번-2번-3번-4번 순서의 우선순위로 this가 결정된다.
- 화살표 함수는 이 조건을 모두 무시하고, 무조건 화살표 함수가 선언된 렉시컬 스코프가 this로 정해진다.

## IIFE (Immediately Invoked Function Expression)
- 함수를 즉시 호출하는 표현식이라는 의미를 가지고 있다.
- `(function () {...})()`이나 `(() => { ... })()`같이 함수 선언문을 소괄호로 둘러싸고, 그 둘러싼 함수 표현식을 `()`를 통해 그 자리에서 바로 호출하는 방식.
- 소괄호로 둘러싸인 IIFE를 연달아 호출하고자 할 때, intermidiate value로 인식되는 문법 오류를 방지하기 위해, IIFE 사이사이를 `;`(세미콜론) 등등으로 구분지어 주어야 한다.

## 고차함수 (또는 일급함수)
- 함수의 파라미터로 전달되는 함수.
- 또는 함수에서 리턴으로 받게 되는 함수.

## 클로저
- 어떤 함수의 리턴으로 받게 되는 일급함수 중, 그 함수 외부에서 접근할 수 없는, 함수 내 지역변수에 접근할 수 있게 해주는 통로 역할을 하는 일급함수.
- 어떻게 이게 가능한 건가?
  - 함수의 실행이 끝나면 실행 컨텍스트가 사라지는데, 이 때 해당 실행 컨텍스트에 남아있던 지역 변수를 참조하는 함수(즉 클로저)가 아직 살아있기 때문에, 가비지 컬렉팅에서 제외되기 때문이다.
- 예시: React의 useState

## 호이스팅
- 함수나 변수가 선언되기 전에 해당 함수나 변수에 접근할 수 있게 하는 JavaScript의 특성 중 하나.

## 스코프
- 함수나 변수에 접근할 수 있는 범위.
- 글로벌 스코프: 어디든지 해당 함수 또는 변수에 접근할 수 있다.
- 지역 스코프: 그 지역 내에서만 해당 함수 또는 변수에 접근할 수 있다.

### 렉시컬 스코프
- 함수나 변수가 선언된 곳의 직속 상위 스코프.

## 구조 분해 할당
- 배열이나 객체를 분해시켜 개별 변수에 할당시키는 방법.
- 예시: const [one, two, three] = [1, 2, 3] 또는 const { yasuo, maverick } = { yasuo: 1, maverick: '222' } 등등.

## spread 연산자와 rest 연산자의 차이
- spread 연산자: ...[...] 또는 ...{...} 연산자를 통해 배열이나 객체에 있는 원소들을 푸는 연산.
- rest 연산자: ...rest 등등의 연산자를 통해 = 연산자의 우항 또는 함수의 파라미터 등등에서 전달받은 나머지를 하나로 묶는 연산이다.

## AJAX (Asynchronus JavaScript And XML)
- JavaScript와 XML을 사용한 비동기적 정보 교환 기능. 
- AJAX의 장점
  - AJAX를 통해, 전체 페이지를 다시 불러오지 않고 페이지의 일부만 바꿈으로써 동적인 웹 페이지를 구현할 수 있다.
  - AJAX를 사용하면, 웹 페이지 일부의 로딩을 기다리지 않고 비동기적으로 페이지 내 다른 활동을 할 수 있다.
- AJAX를 어떻게 할 수 있나?
  - XMLHttpRequest 사용
  - fetch API 사용

## == 연산자와 === 연산자의 차이
- == (느슨한 등가) 연산자: 필요하다면 타입 변환을 하며 두 항의 값이 동일한지 비교하는 연산자이다.
  - 예: undefined == null은 true이며, 1 == '1'도 true이다.
- === (엄격한 등가) 연산자: 타입 변환 없이 strict하게 두 항의 값이 동일한지 비교하는 연산자이다.
  - 예: undefined === null은 false이며, 1 === '1'도 false이다.
- JavaScript에선 === 연산자의 사용이 권장된다.

## 템플릿 리터럴
- \`...\`(백틱)으로 감싸여진, 문자열 사용에 큰 유연성을 더하는 기능으로, 문자열 삽입과 문자열 안에 변수 넣기 등등을 더욱 간단하게 할 수 있다.
- 백틱 내에 ${expression}(플레이스홀더)를 통해 expression 값을 템플릿에 넣어 문자열로 만들 수 있다.
- 예시: const what = 'science'일 경우, \`yasuo is ${what}\` === 'yasuo is science'가 된다.

## 함수

### function 키워드
- `function functionName(...parameters) { ... }`
- 호이스팅 가능.
- 함수 내에서 `this`를 사용하려고 한다면, `.call()`, `.apply()`, `.bind()` 등등으로 this를 지정해야 함.

### 화살표 함수
- `const functionName = (..parameters) => { ... };`
- 기존 함수에 비해 문법이 간결하다.
- `this`가 렉시컬 스코프로 고정됨.
  - 이는 React 클래스 컴포넌트 등등에서 콜백 호출 시 this를 bind할 필요가 없어 매우 유용함.
  - 예시
    - 기존 함수: `<PseudoComponent onclick={function () {}.bind(this)}></PseudoComponent>`
    - 화살표 함수: `<PseudoComponent onclick={() => {}}></PseudoComponent>`
- 호이스팅 불가.
- `=>`의 의미?
  - 파라미터로 이루어진 좌항식을 우항식으로 평가하고 그 결과를 반환시키도록 하는 연산자이다.
  - 우항식은 한 줄 또는 여러 줄이 될 수 있다.

## 비동기 처리

### 콜백 활용
- 비동기 처리 후 실행할 콜백 함수를 파라미터 등등으로 넘기는 방법.
- 예시: setInterval, setTimeout, EventTarget.addEventListener 등등.

### Promise 객체 활용
- Promise 객체를 활용한 비동기 처리 방법
- new Promise((resolve, reject) => { ... })에서, resolve를 통해 성공적인 결과값을 받고, reject를 통해 예외를 던진다.
- 여러 Promise를 다루는데 쓰이는 함수
  - Promise.any
    - 순회 가능한 객체에 대해 주어진 Promise 중 하나만 resolve되어도 될 때 쓰인다.
    - resolve된 경우가 있을 때, 첫번째 resolve를 기준으로 Promise 결과값이 반환된다.
    - 모든 Promise가 reject된 경우, reject된 Promise의 배열을 반환한다.
  - Promise.all
    - 순회 가능한 객체에 대해 주어진 모든 Promise가 resolve되어야 할 때 쓰인다.
    - 모든 Promise가 resolve된 경우, resolve된 Promise의 결과값 배열을 반환한다.
    - reject된 경우가 있을 때, 첫번째 reject를 기준으로 해당 Promise가 reject된다.
  - Promise.allSettled
    - 순회 가능한 객체에 대해 모든 Promise를 실행한 후, 각 Promise의 결과를 나타내는 객체를 반환한다.
    - 성공 여부와 상관없는 비동기 작업들을 수행해야 하는 경우나 각 Promise들의 결과값을 알아야 할 때 유용하게 사용할 수 있다.
  - Promise.race
    - 순회 가능한 객체에 대해 주어진 Promise 중 가장 먼저 결과(resolve든 reject든 상관 없이)가 나온 Promise 결과값을 반환한다.

### async, await 활용
- Async Function 이벤트 루프를 통해 비동기적으로 작동하는 함수이다. 암시적으로 Promise를 사용하여 결과를 반환한다.
- 문법이 간결하고, 구문이 기존 함수와 비슷하며, 콜백 지옥을 쉽게 벗어날 수 있는 비동기 처리 방법이다.
- async 키워드
  - 이 함수는 비동기적으로 실행된다는 것을 선언하는 키워드.
  - 예시: async function asyncFunctionName(...) { ... } 또는 const asyncArrowFunctionName = async (...) => { ... }
- await
  - async 함수 안에서 어떤 비동기 로직이 완료될 때까지 기다리라는 키워드.
  - 예시
    - async function asyncFunctionName(...) { ... await asyncCodes(...); ... }
    - async (...) => { ... await asyncCodes(...); ... }

## Strict Mode
- JavaScript를 Strict Mode로 동작하게 만드는 구문.
- 전역 또는 함수 스코프 최상단에 `'use strict';` 구문을 삽입함으로써 동작한다.
  - JavaScript 모듈은 기본적으로 Strict Mode로 동작한다.
- Strict Mode로 동작할 경우
  - 기존에는 조용히 무시되던 에러들이 Throw된다.
  - ECMAScript에서 차기 정의될 문법의 사용을 금지한다.
  - JavaScript 엔진의 최적화 작업을 어렵게 만드는 실수를 바로잡는다.
    - 글로벌 변수 생성을 금지한다.
    - Write할 수 없는 전역 또는 프로퍼티, getter only 프로퍼티에 대해 새로 할당하는 것을 금지한다. 또한, 확장 불가능하도록 설정된 객체에 새 프로퍼티를 할당하는 것도 금지된다.
    - unique한 함수 파라미터를 요구한다. (function funcName(a, a, c) { ... }에서 에러를 일으킨다)
    - Object.prototype같이 삭제할 수 없는 프로퍼티를 삭제하려는 시도를 금지한다.
    - 8진 구문 사용을 금지한다. (043 같은 8진법 수 금지)
    - 원시 값에 값을 할당하는 것을 금지한다.

## 호스트 객체와 네이티브 객체의 차이
- 호스트 객체
  - 브라우저, Node 등등 실행 환경에 따라 달라지는 객체.
  - 예: 브라우저에서는 window, Node에서는 global 등등.
- 네이티브 객체
  - 실행 환경과 상관없이 동일하게 동작하는 객체.
  - 예: Date 객체 등등.

## JavaScript 개발에 쓰이는 디버깅 툴
- console.log, console.debug, console.error 등등
- Chromium 기반 브라우저(Google Chrome, Microsoft Edge 등등)의 Developer Tools (F12로 불러옴)

## document.onload, DOMContentLoaded

## Polyfill
- 특정 기능을 지원하지 않는 브라우저에서도 동작할 수 있도록 개발자가 구현해놓은 기능에 대한 코드 조각이나 플러그인을 말함.

## 번들러
- JavaScript, CSS, JPG, PNG 등, 여러 개로 나뉘어져 있고 서로 복잡하게 얽힌 각 모듈을 하나의 JavaScript 파일로 묶어주는 프로그램.
- 예시: Webpack, Rollup, Vite, esbuild 등등.

## 커리 (curry)

## SPA (Single Page Application)
- 클라이언트 사이드에서 렌더링되는 애플리케이션.
- 앱이 조금 더 반응성 있게 느껴진다.
- 페이지 깜빡임이나 재로딩 딜레이 없이 다른 페이지로 이동할 수 있다.
- HTML5 History API가 이동 내역을 기억한다.
- 더 적은 HTTP Request가 간다.
- 새 데이터가 필요할 때, AJAX 요청의 결과를 JSON 포맷 형태로 데이터를 가져온다.
- 서버와 클라이언트 사이의 역할 구분이 명확해지므로, 서버를 수정할 필요 없이 다른 플랫폼 앱을 더욱 쉽게 만들 수 있다.
- 초기 로딩 시 불러온 JavaScript 파일을 통해, 데이터와 페이지를 동적으로 갱신한다.
- 초기 로딩 시 초기 페이지 마크업와 함께 프레임워크, 라이브러리, 앱 코드, 스타일시트 등등의 리소스를 로딩한다. 그래서 초기 로딩의 비용이 크다.
- 컨텐츠의 렌더링을 JavaScript에 의존하는데, 이 때 모든 검색 엔진이 크롤링 중에 JavaScript를 실행하지는 않으므로, 검색 엔진 최적화의 장애물이 될 수도 있다.

## 검색 엔진 최적화 (SEO, Search Engine Optimization)
- 검색 엔진 최적화란
  - Google같은 검색 엔진에 친화적인 사이트를 구축하여, 광고가 아닌 자연스러운 검색 결과를 통해 트래픽의 양과 질을 극대화하는 작업.
  - 이 때, 자연스러운 검색 결과란, 광고같이 인위적으로 상위 결과에 올리는 것이 아닌, 사용자들이 순수하게 검색하여 나온 결과를 말한다. 즉, 자연스러운 검색 결과는 비광고성을 띤다.
- 검색 엔진 최적화 방법 (출처: https://library.gabia.com/contents/domain/4359/)
  - 적절한 키워드 본문에 배치하기.
  - 문법에 맞는 HTML 작성하기.
  - 구체적인 페이지 제목 사용하기.
  - 메타 태그 활용.
  - 이미지에 alt 속성 (대체 텍스트) 작성.
  - 중요한 링크를 이미지 맵(이미지에 대한 `<map>` 태그와 `<area>` 태그를 사용하는 것)에 걸어두지 않기.
  - 플래시 전용 페이지 피하기.
  - 주요한 키워드를 `<anchor>` 태그를 사용하여 배치하기.
  - 모든 페이지가 유입 페이지가 될 수 있도록 사이트를 구성.
  - HTTPS 사용.

## 제네레이터 함수
- 제네레이터 함수를 사용하는 이유
  - 필요한 여러 개의 값을 yield를 통해 받아올 수 있어, 이터레이터(이터러블 객체)를 함께 사용하여 데이터 스트림을 만들 수 있다.
  - 다음 yield 등등으로 다음 값을 받을 때까지 계산되지 않으므로, 잠재적으로 무한한 데이터 구조를 정의할 수 있다.
- 제네레이터 함수 예시
  ```javascript
  function* generatorFuncName(...parameters) {
    for (const parameter of parameters) {
      yield parameter;
    }
    return 'finalValue';
  }
  ```
- function 키워드 바로 뒤에 *를 붙임으로써 선언한다.
- 함수 호출 시 generator 객체를 리턴한다. 함수의 로직은 아직 실행되지 않는다.
- .next() 메소드 호출 시 yield 또는 return에 도달할 때 받은 value와 done 여부를 객체 형태로 받는다.
  - yield로 받은 객체는 { value: ..., done: false }
  - return으로 받은 객체는 { value: ..., done: true }
- 함수의 로직이 종료된 이후에도 .next() 메소드를 호출할 수 있지만, 이 겅우 { done: true } 객체를 계속 받게 된다.
- generator 객체는 순회를 할 수 있기(iterable이기) 때문에, for ... of문에 사용될 수 있다.
  - 예시
    ```javascript
    function* generatorFuncName(...parameters) {}
    const generator = genenratorFuncName(...);
    for (const genElement of generator) {
      ...
    }
    ```
  - 이 때, yield로 받은 value만 순회하며, return으로 받은 value는 무시된다.


## 문자열 관련 함수

## 객체 관련 함수
- Object.entries
  - 객체의 [key, value]들을 배열로 반환시킨다.
- Object.keys
  - 객체의 키들을 배열로 반환시킨다.
- Object.values
  - 객체의 값들을 배열로 반환시킨다.

## 배열 관련 함수

- Array.prototype.forEach((value, index) => ...)
  - 배열의 각 엘리먼트에 대해 파라미터로 넘겨진 함수로 일괄적인 로직을 수행한다.
  - 원본 배열을 변경하지 않으며, 결과값을 반환하지 않는다.
- Array.prototype.map((value, index) => ...)
  - 배열의 각 엘리먼트에 대해 파라미터로 넘겨진 함수로 일괄적인 로직을 수행하여 각 결과값을 도출시킨다.
  - 원본 배열을 변경하지 않으며, 배열의 각 엘리먼트에 대한 파라미터 함수의 결과값의 배열을 반환한다.
- Array.prototype.filter((value, index) => ...)
  - 배열의 각 엘리먼트에 대해 파라미터로 넘겨진 함수로 일괄적인 로직을 수행하여 참일 경우에 해당하는 엘리먼트만 추려낸다.
  - 원본 배열을 변경하지 않으며, 각 엘리먼트에 대한 파라미터 함수의 결과값이 참인 경우에 해당한 엘리먼트만으로 이루어진 배열을 반환한다.
- Array.prototype.find((value, index) => ...)
  - 배열의 각 엘리먼트에 대해 파라미터로 넘겨진 함수의 결과값이 참인 엘리먼트를 찾는 함수.
  - 원본 배열을 변경하지 않으며, 각 엘리먼트에 대한 파라미터 함수의 결과값이 참인 가장 첫 번째 엘리먼트를 반환한다.
- Array.prototype.findIndex((value, index) => ...)
  - 배열의 각 엘리먼트에 대해 파라미터로 넘겨진 함수의 결과값이 참인 엘리먼트의 인덱스값을 찾는 함수.
  - 원본 배열을 변경하지 않으며, 각 엘리먼트에 대한 파라미터 함수의 결과값이 참인 가장 첫 번째 엘리먼트의 인덱스값을 반환한다.
- Array.prototype.slice(start, end)
  - 배열의 특정 구간만 추출하는 함수.
  - 원본 배열을 변경하지 않으며, [start, end) 범위에 해당하는 엘리먼트들로 이루어진 배열을 반환한다.
- Array.prototype.splice(start, deleteCount, ...items)
  - 원본 배열을 변경하며, start번째부터 deleteCount개만큼 삭제되고 그 자리에 items가 추가된 배열을 반환한다.
- Array.prototype.sort((lhs, rhs) => ...)
  - 원본 배열을 변경하며, 파라미터 함수에 따라 정렬이 완료된 배열을 반환한다.
- Array.prototype.reduce((acc, value) => ..., init)
  - 원본 배열을 변경하지 않으며, init 값으로 시작하여 각 엘리먼트에 대한 파라미터 함수의 최종 누적 결과값을 반환한다.
- Array.prototype.includes(searchElement, start)
  - 배열에서 특정 엘리먼트가 존재하는지 확인하는 함수.
  - 원본 배열을 변경하지 않으며, start부터 시작하여 searchElement가 있는지 여부를 반환한다.
- Array.prototype.shift()
  - 원본 배열을 변경하며, 배열의 맨 앞에 있었던 엘리먼트를 반환한다.
- Array.prototype.pop()
  - 원본 배열을 변경하며, 배열의 맨 뒤에 있었던 엘리먼트를 반환한다.
- Array.prototype.join(separator)
  - 원본 배열을 변경하지 않으며, separator로 이어진 엘리먼트들의 문자열을 반환한다.
- Array.prototype.concat(...)
  - 원본 배열을 변경하지 않으며, 파라미터로 배열을 순서대로 이어붙인 배열을 반환한다.
  - 파라미터가 없을 수 있으며, 이 때 원본 배열의 복사본을 반환한다.

## Date 관련 함수

## JSON 관련 함수
- JSON.stringify(value)
  - 값의 모든 내용을 JSON 문자열로 만든다.
  - 객체일 경우, 객체 안의 모든 내용까지 문자열로 만든다.
- JSON.parse(text)
  - 주어진 JSON 문자열을 토대로 JavaScript 객체나 값을 만든다.
  - 주어진 문자열이 JSON 문법에 맞지 않으면 에러가 발생한다.

## 값
- Boolean(...)의 ...에 넣었을 때 false가 되는 값: 0, 0n, '', false, undefined, null
- Number(...)의 ...에 넣었을 때 0이 되는 값: 0, 0n, '', false, [], null

## 웹 스토리지 (Web Storage)
- 웹 스토리지란?
  - HTML5에 추가된 스펙 중 하나로, 웹의 데이터를 클라이언트에 저장할 수 있게 만들어주는 저장소.
  - 키와 값이 한 쌍을 이루어 데이터가 저장되며, 키를 기반으로 데이터가 조회된다.
  - 쿠키와의 차이점
    - 쿠키는 데이터가 매 요청마다 헤더를 통해 서버로 전송되지만, 웹 스토리지의 데이터는 전송되지 않는다.
    - 쿠키는 최대 20개에 용량도 4KB 이내여야 한다는 제한이 있지만, 웹 스토리지는 용량과 개수의 제한이 없다.
    - 쿠키는 만료되는 기간이 있으나, 웹 스토리지는 만료되지 않는다.
- 웹 스토리지의 종류
  - localStorage
    - 탭 (또는 브라우저 컨텍스트) 간 데이터 공유도 가능
    - 탭이 종료되어도 데이터가 보존됨
  - sessionStorage
    - 탭 간 데이터 공유 불가
    - 탭이 종료되면 데이터가 소실됨
