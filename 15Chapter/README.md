## 15장  let, const 키워드와 블록 레벨 스코프

---

### 15.1 var 키워드로 선언한 변수의 문제점

---

**15.1.1 변수 중복 선언 허용**

```jsx
var x = 1;
var y = 1;

// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
//초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해 varㅋ 키워드가 없는 것처럼 동작한다.
var x = 100;

//초기화문이 없는 변수 선언문은 무시된다.
var y;

console.log(x); //100
console.log(y); //1
```

**15.1.2 함수 레벨 스코프**

- `var` 키워드로 선언한 변수의 스코프는  블록 레벨 스코프가 아닌 함수 레벨 스코프이다.

```jsx
var x = 1;

if (true) {
 // 지역 스코프를 가지지 않기 때문에 x에 값을 재할당 한다.
 // 값이 의도치 않게 변경된다.
 var x = 10;
}

console.log(x); // 10
```

**15.1.3 변수 호이스팅**

- `var`키워드로 선언한 변수는 런타임 이전 변수 선언과 동시에 초기화 단계가 진행되는데, 변수의 값을 undefined로 초기화 한다.
- 가독성을 떨어뜨리고 오류를 발생시킬 여지를 남긴다.

```jsx
// 이 시점에는 변수 호이스팅에 의해 이미 foo 변수가 선언되었다(1. 선언 단계)
// 변수 foo는 undefined로 초기화된다.(2. 초기화 단계)
console.log(foo); // undefined

// 변수에 값을 할당(3. 할당 단계)
foo = 123;

console.log(foo); // 123;

// 변수 선언은 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 실행된다.
var foo;
```

### 15.2 let 키워드

---

**15.2.1 변수 중복 선언 금지**

- `let` 키워드로 이름이 같은 변수를 중복 선언하면 문법 에러가 발생한다.

**15.2.2 블록 레벨 스코프**

- `let` 키워드로 선언한 변수는 블록 레벨 스코프를 가진다.

```jsx
let foo = 1;
{
 let foo = 2;
 let bar = 3;
}

console.log(foo); // 1
console.log(bar); // RefenceError
```

**15.2.3 변수 호이스팅**

- `let` 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

```jsx
console.log(foo) // ReferenceError
let foo;
```

- let 키워드로 선언한 변수는 선언 단계와 초기화 단계가 분리되어 진행된다.
- 런타임 이전 자바스크립트 엔진에 의해 암묵적으로 선언 단계가 실행된다.
- 변수 선언문에 도달했을 때 초기화 단계가 실행된다.
- 초기화 단계가 실행되기 이전에 변수에 접근하려고 하면 참조 에러가 발생한다.
- 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 `일시적 사각지대` (Temproal Dead Zone)라고 한다.

```jsx
console.log(foo); //ReferenceError

let foo; // 변수 선언문에서 초기화 단계 실행
console.log(foo) // undefined
```

```jsx
let foo = 1;

{
  console.log(foo) // ReferenceError
  let foo = 2;
}
```

- 호이스팅이 발생하지 않는다면 foo 값으로 1을 출력해야 하지만 호이스팅으로 참조에러가 발생한다.

**15.2.4 전역 객체와 let**

- let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다.

```jsx
let x = 1;

// let, const로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아니다.
console.log(window.x); undefined
```

### 15.3 const 키워드

---

**15.3.1 전역 객체와 let**

- const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화 해야된다. 그렇지 않으면 문법 에러가 발생한다.

```jsx
const foo = 1;
```

- 블록 레벨 스코프를 가지며, 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

**15.3.2 재할당 금지**

- const 키워드로 선언한 변수는 재할당이 금지된다.

```jsx
const foo = 1;
foo = 2; //TypeError
```

**15.3.3 상수**

- 상태 유지와 가독성, 유지보수의 편의를 위해 const 키워드를 사용한다.

```jsx
//변수 이름을 대문자로 선언해 상수임을 명확히 나타낸다.
const TAX_RATE = 0.1;

let preTaxPrice = 100;
let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);

```

**15.3.4 const 키워드와 객체**

- const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다.
- const 키워드는 재할당을 금지할 뿐 불변을 의미하지 않는다.

```jsx
const person ={
 name: "Lee"
};

person.name = 'Park';
console.log(person.name) // Park
```