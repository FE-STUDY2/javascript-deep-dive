# 09 타입 변환과 단축 평가

## 암묵적 타입 변환

- 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는 것.

- 암묵적 타입 변환은 기존 변수 값을 재할당하여 변경하는 것이 아니라 새로운 타입의 값을 만들어 단 한 번 사용하고 버린다.

```jsx
var x = 10
// 암묵적 타입 변환

var str = x + ''
console.log(typeof str, str) // string 10

// x변수의 값이 변경된 것은 아니다.
console.log(typeof x, x) //number 10
```

### 문자열 타입으로 변환
```jsx
1 + '2' // -> '12'

// 템플릿 리터럴은 암묵적으로 문자열 타입
`1 +1 = ${1 + 1}` // -> "1 + 1 = 2"

// 숫자 타입
0 + ''         // -> "0"
-0 + ''        // -> "0"
1 + ''         // -> "1"
-1 + ''        // -> "-1"
NaN + ''       // -> "NaN"
Infinity + ''  // -> "Infinity"
-Infinity + '' // -> "-Infinity"

// 불리언 타입
true + ''  // -> "true"
false + '' // -> "false"

// null 타입
null + '' // -> "null"

// undefined 타입
undefined + '' // -> "undefined"

// 심벌 타입
(Symbol()) + '' // -> TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''           // -> "[object Object]"
Math + ''           // -> "[object Math]"
[] + ''             // -> ""
[10, 20] + ''       // -> "10,20"
(function(){}) + '' // -> "function(){}"
Array + ''          // -> "function Array() { [native code] }"
```

### 숫자 타입으로 변환
```jsx
1 - '1'   // -> 0
1 * '10'  // -> 10
1 / 'one' // -> NaN
```

### 불리언 타입으로 변환
```jsx
if ('')    console.log('1');
if (true)  console.log('2');
if (0)     console.log('3');
if ('str') console.log('4');
if (null)  console.log('5');

// 2 4
```

> 자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy, Falsy 값으로 구분한다
- 아래 값들은 false로 평가되는 Falsy값이다
    - false
    - undefined
    - null
    - 0, -0
    - NaN
    - ‘ ’(빈 문자열)


## 명시적 타입 변환

- 명시적으로 타입을 변경하는 방법은 표준 빌트인 생성자 함수를 new 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법, 암묵적 타입 변환을 이용하는 방법 등이 있다.

### 문자열 타입으로 변환
- 문자열이 아닌 값을 문자열 타입으로 변환하는 방법
1. string 생성자 함수를 new 연산자 없이 호출하는 방법
2. Object.prototype.toString 메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

```jsx
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 => 문자열 타입
String(1)        // -> "1"
String(NaN)      // -> "NaN"
String(Infinity) // -> "Infinity"

// 불리언 타입 => 문자열 타입
String(true)     // -> "true"
String(false)    // -> "false"

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 => 문자열 타입
(1).toString()        // -> "1"
(NaN).toString()      // -> "NaN"
(Infinity).toString() // -> "Infinity"

// 불리언 타입 => 문자열 타입
(true).toString()     // -> "true"
(false).toString()    // -> "false"

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 => 문자열 타입
1 + ''        // -> "1"
NaN + ''      // -> "NaN"
Infinity + '' // -> "Infinity"

// 불리언 타입 => 문자열 타입
true + ''     // -> "true"
false + ''    // -> "false"
```

### 숫자 타입으로 변환
- 숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법
1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. parseInt, parseFloat 함수를 사용하는 방법
3. +단항 산술 연산자를 이용하는 방법
4. *산술 연산자를 이용하는 방법

```jsx
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 숫자 타입
Number('0')     // -> 0
Number('-1')    // -> -1
Number('10.53') // -> 10.53
// 불리언 타입 => 숫자 타입
Number(true)    // -> 1
Number(false)   // -> 0

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 변환 가능)
// 문자열 타입 => 숫자 타입
parseInt('0')       // -> 0
parseInt('-1')      // -> -1
parseFloat('10.53') // -> 10.53

// 3. + 단항 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
+'0'     // -> 0
+'-1'    // -> -1
+'10.53' // -> 10.53
// 불리언 타입 => 숫자 타입
+true    // -> 1
+false   // -> 0

// 4. * 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
'0' * 1     // -> 0
'-1' * 1    // -> -1
'10.53' * 1 // -> 10.53
// 불리언 타입 => 숫자 타입
true * 1    // -> 1
false * 1   // -> 0
```

### 불리언 타입으로 변환
- 불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법
1. Boolean 생성자 함수를 연산자 없이 호출하는 방법
2. !부정 논리 연산자를 두번 사용하는 방법

```jsx
// 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 불리언 타입
Boolean('x')       // -> true
Boolean('')        // -> false
Boolean('false')   // -> true

// 숫자 타입 => 불리언 타입
Boolean(0)         // -> false
Boolean(1)         // -> true
Boolean(NaN)       // -> false
Boolean(Infinity)  // -> true

// null 타입 => 불리언 타입
Boolean(null)      // -> false

// undefined 타입 => 불리언 타입
Boolean(undefined) // -> false

// 객체 타입 => 불리언 타입
Boolean({})        // -> true
Boolean([])        // -> true

// 2. ! 부정 논리 연산자를 두번 사용하는 방법
// 문자열 타입 => 불리언 타입
!!'x'       // -> true
!!''        // -> false
!!'false'   // -> true

// 숫자 타입 => 불리언 타입
!!0         // -> false
!!1         // -> true
!!NaN       // -> false
!!Infinity  // -> true

// null 타입 => 불리언 타입
!!null      // -> false

// undefined 타입 => 불리언 타입
!!undefined // -> false

// 객체 타입 => 불리언 타입
!!{}        // -> true
!![]        // -> true
```

***

## 단축 평가	

### 논리 연산자를 사용한 단축 평가

```jsx
'cat' && 'dog' // -> 'dog'
'cat' && false // -> false
//&& 연산자는 두 개의 피연산자가 모두 true일 때 true를 반환한다

'cat' || 'dog' // -> 'cat'
'cat' || true // -> true
//||연산자는 하나라도 true이면 true를 반환한다

// 논리합(||) 연산자
'Cat' || 'Dog'  // -> "Cat"
false || 'Dog'  // -> "Dog"
'Cat' || false  // -> "Cat"

// 논리곱(&&) 연산자
'Cat' && 'Dog'  // -> "Dog"
false && 'Dog'  // -> false
'Cat' && false  // -> false
```

- 어떤 조건이 Truthy 값인 경우 `&&`연산자 표현식으로 `if`문을 대체할 수 있다

```jsx
var done = true
var message = ''

// 주어진 조건이 true일 때
if (done) message = '완료'

// if 문은 단축 평가로 대체 가능하다.
// done이 true라면 message에 '완료'를 할당
message = done && '완료'
console.log(message) // 완료
```

- 조건이 Falsy 값인 경우 `||` 연산자 표현식으로 `if`문을 대체할 수 있다
```jsx
var done = false
var message = ''

// 주어진 조건이 false일 때
if (!done) message = '미완료'

// if 문은 단축 평가로 대체 가능하다.
// done이 false라면 message에 '미완료'를 할당
message = done || '미완료'
console.log(message) // 미완료
```

- 삼항 조건 연산자는 `if..else`문을 대체할 수 있다
```jsx
var done = true
var message = ''

// if...else 문
if (done) message = '완료'
else      message = '미완료'
console.log(message) // 완료

// if...else 문은 삼항 조건 연산자로 대체 가능하다.
message = done ? '완료' : '미완료'
console.log(message) // 완료
```


> 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때
```jsx
var elem = null
var value = elem.value // TypeError: Cannot read property 'value' of null

// 이때 단축 평가를 사용하면 에러를 발생시키지 않는다.
var elem = null
// elem이 null이나 undefined와 같은 Falsy 값이면 elem으로 평가되고
// elem이 Truthy 값이면 elem.value로 평가된다.
var value = elem && elem.value // -> null
```


> 함수 매개변수에 기본값을 설정할 때
- 함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당되는데, 단축 평가를 사용하면 이를 방지할 수 있다.

```jsx
// 단축 평가를 사용한 매개변수의 기본값 설정
function getStringLength(str) {
  str = str || ''  // 단축 평가
  return str.length
}

getStringLength()     // -> 0
getStringLength('hi') // -> 2


// ES6의 매개변수의 기본값 설정
function getStringLength(str = '') {
  return str.length
}

getStringLength()     // -> 0
getStringLength('hi') // -> 2
```


### 옵셔널 체이닝 연산자
- ES11(ECMAScript2020)에 도입된 null 병합(nullish coalescing)연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.

```jsx
var elem = null

//elem이 null 또는 undefined이면 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어간다
var value = elem?.value
console.log(value)        // undefined
```

- 옵셔널 체이닝 연산자 ?.는 좌항 피연산자가 false로 평가되는 Falsy 값이라도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어간다

```jsx
var str = ''

var length = str?.length
console.log(length) // 0
```


### null 병합 연산자
- ES11(ECMAScript2020)에 도입된 null 병합(nullish coalescing)연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.

```jsx
// 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고,
// 그렇지 않으면 좌항의 피연산자를 반환한다.
var foo = null ?? 'default string'
console.log(foo) // "default string"
```

null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용하다. null 병합 연산자 ??가 도입되기 이전에는
논리 연산자 `||`을 사용한 단축 평가를 통해 변수에 기본값을 설정했다.
논리 연산자 `||`을 사용한 단축평가의 경우 좌항의 피연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, -0, NaN, '')이면 우항의 피연산자를 반환한다.
만약 Falsy 값인 0이나 ''도 기본값으로서 유요하다면 예기치 않은 동작이 방샐할 수 있다.

```jsx
// Falsy 값인 0이나 ''도 기본값으로서 유효하다면 예기치 않은 동작이 발생할 수 있다.
var foo = '' || 'default string'
console.log(foo) // "default string"


// 좌항의 피연산자가 Falsy 값이라도 null 또는 undefined이 아니면 좌항의 피연산자를 반환한다.
var foo = '' ?? 'default string'
console.log(foo); // ""
```
