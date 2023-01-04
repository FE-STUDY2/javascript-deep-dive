# 데이터 타입

- 데이터 타입(Data type) : 프로그래밍 언어에서 사용할 수 있는 데이터의 종류.

## 원시 타입(Primitive Data Type)

### 숫자(Number)

숫자 타입은 **부동소수점(Floating Point) 형식**을 따름.
![부동소수점](https://velog.velcdn.com/images/modolee/post/a830c5e9-ec15-4937-b2d8-6e0dd0ae4370/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-09-08%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.57.48.png)
- 모든 **실수로 처리**(정수, 실수, 2진수, 8진수, 16진수 리터럴은 2진수로 저장되며, 
  데이터 타입을  제공 하지 않기 때문에 이들 값을 참조하면 **10진수로 해석**)

``` js
 let integer = 10;
 let double = 10.12;
 let negative = -20;
```

- 정수로 표시되는 수끼리 나누더라도 실수가 나올 수 있음(자바스크립트는 정수만 위한 타입이 없고  모든 수를 실수로 처리하기때문)


``` js
console.log( 1 === 1.0); // true
```


- Infinity: 양의 무한대
- -Infinity: 음의 무한대 
- NaN(Not a Number): 산술 연산 불가 

```js
 cosole.log(10/0); // Infinity
 cosole.log(10/-0); // -Infinity
 cosole.log(1 * 'String') // NaN
```

### 문자열(String)

텍스트 데이터를 나타낼 때 사용

- 문자열은 **따옴표**로 텍스트를 감싼다

```js
let string = '문자열'; // 작은 따옴표
let str = "문자열"; // 큰 따옴표
let stringText = `문자열`; // 백틱

```

- 자바스크립트에서 가장 일반적인 표기법은 **작은 따옴표**를 사용하는 것(큰따옴표 사용시 쉬프트를 눌러야해 조금더 효율성을 높이고자)

```js
let stringText = '작은 따옴표로 감싼 문자열 내의 "큰 따옴표"는 문자열로 인식한다';
let StringText = "큰 따옴표로로 감싼 문자열 내의 '작은 따옴표'는 문자열로 인식한다";

```
위에 예제처럼 문자열을 따옴표로 감싸는 이유는 키워드나 식별자 같은 토큰을 구분하기 위해서이다. 

```js
// 따옴표로 감싸지 않은 hello를 식별자로 인식
let string = hello; //ReferenceError: hello is not defined
```
만약 따옴표로 감싸지 않으면 자바스크립트 엔진은 키워드나 식별자 같은 토큰으로 인식.
그리고 만약 따옴표로 문자열을 감싸지 않으면 스페이스와 같은 공백 문자도 포함시킬 수 없음.

자바스크립트 문자열은 원시 타입이며, 변경 불가능한 값이며, 이것은 문자열이 생성되면 그 문자열을 변경할수 없다는 걸 의미.

#### 템플릿 리터럴 

- 템플릿 리터럴 : 멀티라인 문자열, 표현식 삽입 태그드 탬플릿 등 편리한 문자열 처리 기능을 제공.
 - 런타임에서 일반 문자열로 변환되어 처리됨
 - 일반 문자열과 비슷해 보이지만 작은( ' ' )/큰 따옴표( " " ) 대신 백틱을 사용( ` ` ).  

```js
let template = `Template literal`;
console.log(template); // Template literal
```

###### 멀티라인 문자열

- 일반 문자열 내에서는 줄바꿈(개행)이 허용되지 않음 

```js
let str = 'Hello
world';
//SyntaxError: Invalid or unespected token.
```
따라서 일반 문자열 내에서 줄바꿈 등의 공백을 표현하려면 백슬래쉬( \ )로 시작하는 이스케이프 시퀀스를 사용해야함

밑에 표는 이스케이프 시퀀스 

|이스케이프 시퀀스|의미|
|----------------|---|
|\0|Null|
|\b|백스페이스|
|\f|폼 피드: 프린터로 출력할 경우 |
|\n|개행 다음행으로 이동|
|\r|개행 커서를 처음으로 이동|
|\t|탭 수평|
|\v|탭 수직|
|\uXXX|유니코드 |
|\'|작은 따옴효|
|\"|큰따옴표|
|\\|백슬래쉬|

예시 줄바꿈과 들여쓰기가 적용된 HTML문자열은 다음과 같이 이스케이프 시퀀르를 사용해 작성

```js
let template ='<ul>\n\t<li><a href="#">Home</a></li>\n</ul>';
console.log(template);
```
```html
<ul><li><a href = "#" >Home</a></li></ul>
```
일반 문자열과 달리 템플릿 리터럴 내에서는 이스케이프 시퀀스를 사용하지 않고 줄바꿈이 허용되며,
공백이 있는 그대로 적용

```js
let template =`<ul>
<li><a href="#">Home</a></li>\n</ul>`;
console.log(template);
```

##### 표현식 삽입 

문자열은 문자열 연산자 **+**를 사용해 연결 가능 

- + 연산자는 피연산자줃ㅇ 하나의 이상이 문자열인 경우 문자열 연결 연산자로 동작, 그외에는 덧셈 연산자로 동작 

```js
let first = 'Ung-mo';
let last = 'Lee';

//ES5: 문자열 연결
console.log('My name is' + first + ' ' + last + '.');//My name is Lee Ung-mo.
```

- 표현식 삽입을 통해 간단히 문자열을 삽입 가능 (문자열 연산자 보다 가독성 좋고 간편하게 문자열 조합 가능)

```js
let first = 'Ung-mo';
let last = 'Lee';

//ES5: 문자열 연결
console.log(`My name is' + ${first} + ' ' + ${last} + '.'`);//My name is Lee Ung-mo.
```
- 표현식 삽입시 예제처럼 ${}으로 표현식을 감싼다.(표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입 강제로 변환되어 삽입.)

```js
console.log(`1 + 2 = ${ 1+ 2}`)// 1 + 2 = 3
```

- 탬플릿 리터럴이 아닌 일반 문자열에서 표현식 삽입은 문자열로 취급 

```js
console.log('1 + 2 = ${ 1+ 2}')// 1 + 2 = ${ 1 + 2}
```

### 불리언 

논리적인 참(True),거짓(false) 두가지 뿐이다 

```js
let foo = true;
console.log(foo); //true

foo = false;

console.log(foo); // false
```

- 참과 거짓으로 구분 되는 조건에 의해 프로그램의 흐름을 제어하는 조건 문에서 자주 사용

### undefined

- undefined 타입은 undefined가 유일 
- var 키워드로 선언한 변수는 암묵적으로 undefined로 초기화(변수 선언에 의해 확보된 메모리 공간 을 처음 할당이 이뤄질때까지 빈상태 내버려두지 않고 자바스크립트 엔진이 undefined로 초기화) 따라서 변수를 선언한 후 초기화 하지 않은 변수를 참조하면 undefined가 반환


```js
var foo;

console.log(foo); // undefined
```

이처럼 자바스크립트 엔진이 변수를 초기화 할때 사용하는 값, 변수를 참조했을 때 undefined가 반환된다면 참조한 변수가 선언 이후 갓이 할당된 적 없는  즉 초기화 되지 않는 변수라는 것을 간파 가능

### null

- null
- 변수에 값이 없다는 것으로 의도적인 명시 할때 사용(변수에 null 할당시 변수가 이전에 참조 하던 값을 더 이상 참조하지 않겠다는 의미, 값에 대한 참조를 명시적으로 제거하는 것을 의미, 자바스크립트 엔진은 누구도 참조하지 않는 메모리 공간에 대해 강비지 콜랙션을 수행)

```js
var foo = 'Lee';
foo = null; 
```
함수가 유효한 값을 반환할 수 없는 경우 명시적으로 null을 반환하기도 한다. 

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var element = document.querySelector('.myClass')
        console.log(element);// html에 myClass클래스를 갖는 요소가 없다면 null을 반환
    </script>
</body>
</html>
```

### 심벌 타입

- 다른 값과 중복 되지 않은 유일 무이한 값. 
- 따라서 주로 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용
- 심벌 함수를 호출해 생성(이때 생성된 심벌 값은 외부에 노출 되지 않으며, 다른 값과 절대 중복이 되지않은 유일무이한 값)

```js
//심볼 생성
var key = Symbol('key');
console.log(typeof key);//Symbol
// 객체 생성
var obj = {};
// 이름이 충돌할 위험이 없는 값인 심벌은 프로퍼티 키로 사용한다 
obj[key] ='value';
console.log(obj[key])
```

###  Biglnt

- BigInt는 길이 제한이 없는 정수(integer)
-숫자(number) 데이터가 안정적으로 표시할 수 있는 최대치(2^53 - 1)보다 큰 정수를 표현
-정수 뒤에 n을 붙이거나 BigInt()를 호출해 생성
```js
console.log(1234567890123456789012345678901234567890)
// 1.2345678901234568e+39

console.log(1234567890123456789012345678901234567890n)
console.log(BigInt('1234567890123456789012345678901234567890'))
// 1234567890123456789012345678901234567890n
```
## 객체 타입

### 배열
'Apple'이나 'Banana' 같은 데이터를 배열의 아이템(Item) 혹은 요소(Element)라고 부름.

```js
let fruits

// 생성자
fruits = new Array('Apple', 'Banana', 'Cherry')

// 리터럴
fruits = ['Apple', 'Banana', 'Cherry']

// 배열의 아이템 인덱싱
console.log(fruits[1]) // 'Banana'

// 배열의 길이
console.log(fruits.length) // 3

// 첫 번째 아이템 인덱싱
console.log(fruits[0]) // 'Apple'

// 마지막 아이템 인덱싱
console.log(fruits[fruits.length - 1]) // 'Cherry'
```


### 객채
Key:Value(속성:값) 형태로 더 복잡한 데이터 구조를 나타낼 때 사용

```js
let user

// 생성자1
user = new Object()
user.name = 'HEROPY'
user.age = 85

// 생성자2
function User() {
  this.name = 'HEROPY'
  this.age = 85
}
user = new User()

// 리터럴
user = {
  name: 'HEROPY',
  age: 85
}

console.log(user.name) // 'HEROPY'
console.log(user.age) // 85
```

### 함수

자바스크립트에서 함수(function)는 1급 객체(First-class object)로,
하나의 값으로 변수나 인수 혹은 반환이 가능

```js
function a() {
  return 123
}

console.log(typeof a) // function
console.log(typeof a()) // number

console.log(a) // f a() { return 123 } 
console.log(a()) // 123
```

#### 데이터 타입의 필요성
 
##### 데이터 타입에 의한 메모리 공간 확보와 참조

- 자바스크립트 엔진은 변수에 할당되는 값이 데이터 타입에 따라 메모리 공간의 크기를 결정 

##### 데이터 타입에 의한 값 해석

- 값 저장시 메모리 공간의 크기를 결정하기 위해서 
- 값을 참조할 때 한번에 읽어들여야 할 메모리 공간의 크기를 결정하기 위해
- 메모리에 읽어 들인 2진수는 어떻게 해석할지 결정

#### 동적 타이핑 

##### 동적 타입 언어와 정적 타입 언어

- 정적 타입 언어: 변수를 할당 시 값의 종류, 즉 데이터 타입을 사전에 선언해야 한다(이를 명시적 타입 선언)


```JS
var foo;
console.log(typeof foo);// undefined

foo = 3;
console.log(typeof foo);//number

foo = 'Hello';
console.log(typeof foo); //string

foo = true;
console.log(typeof foo); //boolean

foo = null;
console.log(typeof foo); //object

foo = Symbol();
console.log(typeof foo); //symbol

foo = {};
console.log(typeof foo); //object

foo = [];
console.log(typeof foo); //object

foo = function() {};
console.log(typeof foo); //function
```
typeof 연산자로 변수를 연산 하면 변수의 데이터 타입 반환 (변수에 할당된 값의 데이터 타입을 반환)

자바스크립트(동적 타입의 언어)의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론)된다. 재할당에 의해 변수의 타입은 언제든지 동적으로 변할수 있다.(동적 타이핑)

#### 동적 타입 언어와 변수 
변수 사용시 주의


- 변수는 꼭 필요한 경우 제한적으로 사용.
- 변수의 유효범위는 최대한 좁개 만들어 변수의 부작용 억제 
- 전역 변수를 최대한 사용하지 않는다 
- 변수보다 상수를 사용해 값의 변경을 억제
- 변수 이름은 목적이나 의미를 파악 할수 있는 네이밍.