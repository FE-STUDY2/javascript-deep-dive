## 14장  전역 변수의 문제점

---

### 14.1 변수의 생명 주기

---

**14.1.1 지역 변수의 생명 주기**

- 변수는 생성되고 소멸되는 생명 주기가 있다.
- 전역 변수의 생명 주기는 애플리케이션의 생명 주기와 같다.
- 함수 내부의 지역 변수는 함수가 호출되면 생성되고 함수가 종료되면 소멸한다. 지역 변수의 생명 주기는 함수의 생명 주기가 같다.

```jsx
function foo() {
  var x = "local";
  console.log(x); // local
  return x;
}

foo();
console.log(x);
```

- foo 함수를 호출하지 않으면 함수 내부의 변수 선언문이 실행되지 않는다
- 호이스팅은 스코프 단위로 동작한다.

**14.1.2 전역 변수의 생명 주기**

- 전역 코드는 함수 호출과 같이 전역 코드를 실행하는 특별한 진입점이 없고 코드가 로드되자마자 곧바로 해석되고 실행 된다.
- 전역 코드는 반환문을 사용할 수 없으므로 마지막 문이 실행되어 더 이상 실행될 문이 없을 때 종료한다.
- var 키워드로 선언한 전역변수는 window의 프로퍼티이다.
- var 키워드로 선언한 전역 변수의 생명 주기는 전역 객체의 생명 주기와 일치한다.

### 14.2 전역 변수의 문제점

---

**암묵적 결합**

- 전역 변수는 코드 어디서든 참조하고 할당할 수 있다.
- 이는 모든 코드가 전역 변수를 참조하고 변경할 수 있는 **암묵적 결합**을 허용하는 것이다.
- 변수의 유효 범위가 커질수록 코드의 가독성은 나빠지고 위험성은 높아진다.

**긴 생명 주기**

- 전역 변수는 생명주기가 길다.
- 따라서 메모리 리소스도 오랜 기간 소비하게 된다.
- var 키워드는 변수의 중복 선언을 허용하므로 변수 이름이 중복될 가능성이 있어 의도치 않은 재할당이 이루어진다.

**스코프 체인 상에서 종점에 존재**

- 전역 변수는 스코프 체인 상에서 종점에 존재한다.
- 즉, 전역 변수의 검색 속도가 가장 느리다.

**네임스페이스 오염**

- 자바스크립트는 파일이 분리되어 있어도 하나의 전역 스코프를 공유한다.
- 따라서 다른 파일 내에서 동일한 이름으로 명명된 전역 변수가 존재할 경우 예상치 못한 결과를 가져올 수 있다.

### 14.3 전역 변수의 사용을 억제하는 방법

---

- 전역 변수를 반드시 사용해야 할 이유를 찾지 못한다면 지역 변수를 사용해야 한다.
- 변수의 스코프는 좁을수록 좋다.

**14.3.1** **즉시 실행 함수**

- 모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수가 된다.

```jsx
(function () {
  var x = 10;
})();

console.log(x); //ReferenceError
```

**14.3.2 네임스페이스 객체**

- 전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 방법.
- 네임스페이스 객체가 전역 변수에 할당되므로 그다지 유용하지 않다.

```jsx
var MYAPP = {};

MYAPP.person = {
  name: "LEE",
  address: "seoul",
};

console.log(MYAPP.person.name); // LEE
```

**14.3.3 모듈 패턴**

- 모듈 패턴은 관련 있는 변수와 함수를 모아 즉시 실행 함수로 감싸 하나의 모듈을 만든다.
- 모듈 패턴은 클로저를 기반으로 동작 한다.
- 모듈 패턴은 전역 변수를 억제할 수 있으며 캡슐화까지 구현할 수 있다.

```jsx
var Counter = (function () {
  var num = 0; // private 변수

  // 외부로 공개할 데이터나 메서드
  return {
    increase() {
      return ++num;
    },
    decrease() {
      return --num;
    },
  };
})();

console.log(Counter.num); // undefined
console.log(Counter.increase()); // 1
```

**14.3.4 ES6 모듈**

- **ES6 모듈은 파일 자체의 독자적인 모듈 스코프를 제공한다.** 모듈 내에서 var 키워드로 선언한 변수는  전역 변수가 아니게 된다.
- ES6 모듈을 사용하기 위해서는 `<script>` 태그에 `type="module"` 어트리뷰트를 추가하면 된다. 모듈의 파일 확장자는 `mjs`를 권장한다.

```jsx
<script type="module" src="./lib.mjs"></script>
```

- ES6 모듈은 IE를 포함한 구형 브라우저에서는 동작하지 않는다.
- 때문에 아직까지는 브라우저가 지원하는 ES6 모듈 기능보다는 Webpack등의 모듈 번들러를 사용하는 것이 일반적이다.

###