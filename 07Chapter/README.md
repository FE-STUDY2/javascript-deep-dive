## 07장 연산자


### 7-1 산술 연산자
- 이항 산술 연산자

> 이상 산술 연산자는 2개의 피연산자를 연산하여 숫자 값을 만든다

|이상 산술 연산자|의미|부수효과|
|:---:|:---:|:---:|
| + |덧셈| X |
| - |뺄셈| X |
| * |곱셈| X |
| / |나눗셈| X |
|%|나머지|X|

```jsx
5 + 2 // -> 7
5 - 2 // -> 3
5 * 2 // -> 10
5 / 2 // -> 2.5
5 % 2 // -> 1
``` 

- 단항 산술 연산자

> 1개의 피연산자를 연산하여 숫자 값을 만든다

|단항 산술 연산자|의미|부수 효과|
|:---:|:---:|:---:|
|++|증가|O|
|--|감소|O|
|+|효과X|X|
|-|양수 <-> 음수|X|

```jsx
var x = 5, result

// 선할당 후증가
result = x++
console.log(result, x) // 5 6

// 선증가 후할당
result = ++x
console.log(result, x) // 7 7

// 선할당 후증가
result = x--
xonsole.log(restul, x) // 7 6

// 선감소 후할당
result = --x
console.log(result, x) // 5 5

// 아무런 효과X
+10 // 10
+(-10) //-10 
```

- 숫자 타입이 아닌 피연산자에 + 연산자를 사용하면 피연산자를 숫자 타입으로 변환하여 반환한다
```jsx
var x  = '1'

// 문자열을 숫자로 타입 변환한다.
console.log(+x) // 1
// 부수 효과는 없다.
console.log(x)  // "1"

// 불리언 값을 숫자로 타입 변환한다.
x = true;
console.log(+x) // 1
// 부수 효과는 없다.
console.log(x)  // true

// 불리언 값을 숫자로 타입 변환한다.
x = false;
console.log(+x) // 0
// 부수 효과는 없다.
console.log(x)  // false

// 문자열을 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
x = 'Hello'
console.log(+x) // NaN
// 부수 효과는 없다.
console.log(x)  // "Hello"
``` 

### 7-2 할당 연산자

|할당 연산자|예|동일 표현|부수 효과|
|---|---|---|---|---|
|+=|x += 5|x = x +5|O|


```jsx
var x

x += 5; // x = x + 5
console.log(x) // 15

x -= 5 // x = x - 5
console.log(x) // 10

// 문자열 연결 연산자
str += 'Lee' // str = str + 'Lee'
console.log(str) // 'My name is Lee'
```

### 7-3 비교 연산자
|비교 연산자|의미|사례|설명|
|---|---|---|---|---|
|===|일치 비교|x === y|x, y 값과 타입이 같음|
|!==|불일치 비교|x !== y|x, y값과 타입이 다름|

```jsx
// NaN은 자신과 일치하지 않는 유일한 값이다!
NaN === NaN // false
```

### 7-4 삼항 조건 연산자

> 조건식 ? true일 때 값 : false일 때 값

```jsx
var x = 2

// 2 % 2는 0이고 0은 false로 암묵적 타입 변환된다.
var result = x % 2 ? '홀수' : '짝수'

console.log(result) // 짝수
```

### 7-5 논리 연산자

```jsx
// 논리합(||) 연산자
true || true   // -> true
true || false  // -> true
false || true  // -> true
false || false // -> false

// 논리곱(&&) 연산자
true && true   // -> true
true && false  // -> false
false && true  // -> false
false && false // -> false

// 논리 부정(!) 연산자
!true  // -> false
!false // -> true
```

### 7-6 쉼표 연산자
- 왼쪽 피연산자부터 평가하고 마지막 피연산자의 결과를 반환

```jsx
var x, y, z

x = 1, y = 2, z = 3
```

### 7-7 그룹 연산자
- 그룹 연산자를 사용하면 우선순위를 조절할 수 있다
```jsx
10 * 2 +3 // 23
10 * (2 +3) //50
```

### 7-8 typeof 연산자
```jsx
typeof ''              // -> "string"
typeof 1               // -> "number"
typeof NaN             // -> "number"
typeof true            // -> "boolean"
typeof undefined       // -> "undefined"
typeof Symbol()        // -> "symbol"
typeof null            // -> "object"
typeof []              // -> "object"
typeof {}              // -> "object"
typeof new Date()      // -> "object"
typeof /test/gi        // -> "object"
typeof function () {}  // -> "function"
```

