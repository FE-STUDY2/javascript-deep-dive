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


