## 12장

---

### 12-1. 함수를 사용하는 이유

- 사용 이유: 코드의 재사용성

### 12-3. 함수 리터럴

- 함수와 일반 객체의 차이:
  - 일반 객체: 호출x
  - 함수: 호출o

### 12-4. 함수의 정의 방식

- 함수 선언문

```javascript
function foo(x, y) {
  return x + y;
}
```

- 함수 표현식

```javascript
var add = function (x, y) {
  return x + y;
};
```

- Function 생성자 함수

```javascript
var add = new Function("x", "y", "return x+y");
```

- 화살표 함수

```javascript
var add = (x, y) => x + y;
```

- 함수 호이스팅

  - 함수 표현식으로 호출하면 변수 호이스팅은 일어나지만 함수 호이스팅은 일어나지 않고 함수 선언문으로 호출하면 함수 호이스팅이 일어난다.
  - ```javascript
    console.log(add(2, 5)); //7
    console.log(sub(2, 5)); //error
    function add(x, y) {
      return x + y;
    }
    var sub = function (x, y) {
      return x - y;
    };
    ```

### 12-7. 다양한 함수 형태

- 즉시 실행 함수

```javascript
// 익명 즉시 실행 함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
})();
```

- 재귀함수

```javascript
// 팩토리얼(계승)은 1부터 자신까지의 모든 양의 정수의 곱이다.
// n! = 1 * 2 * ... * (n-1) * n
function factorial(n) {
  // 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춘다.
  if (n <= 1) return 1;
  // 재귀 호출
  return n * factorial(n - 1);
}

console.log(factorial(0)); // 0! = 1
console.log(factorial(1)); // 1! = 1
console.log(factorial(2)); // 2! = 2 * 1 = 2
console.log(factorial(3)); // 3! = 3 * 2 * 1 = 6
console.log(factorial(4)); // 4! = 4 * 3 * 2 * 1 = 24
console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

- 중첩함수

```javascript
function outer() {
  var x = 1;

  // 중첩 함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x + y); // 3
  }

  inner();
}

outer();
```

- 콜백함수

```javascript
// 외부에서 전달받은 f를 n만큼 반복 호출한다.
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i); // i를 전달하면서 f를 호출
  }
}

var logAll = function (i) {
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3
```

- 순수함수와 비순수함수

```javascript
var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
  return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2

var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화한다.

// 비순수 함수
function increase() {
  return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```

- 함수형 프로그래밍란?
  - 순수함수와 보조함수를 통해 외부상태가 변경하는 부수효과를 지양하고 불변성을 지향하는 패러다임
