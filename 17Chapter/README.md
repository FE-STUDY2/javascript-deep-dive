# 17장 생성자 함수에 의한 객체 생성

## **17장 생성자 함수에 의한 객체 생성**

---

### **17.1 Object 생성자 함수**

---

- 생성자 함수는 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수이다.
- new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.
- 자바스크립트는 Object 생성자 함수 이외에도 String, Number, Boolean, Function, Array등의 빌트인 생성자 함수를 제공한다.

### **17.2 생성자 함수**

---

**17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제**

- 동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.

**17.2.2 생성자 함수에 의한 객체 생성 방식의 장점**

- 생성자 함수에 의한 객체 생성 방식은 마치 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.
- new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다

**17.2.3 생성자 함수의 인스턴스 생성 과정**

1. **인스턴스 생성과 this 바인딩 -**암묵적으로 생성된 빈 객체 인스턴스가 this에 바인딩(this와 this가 가리킬 객체를 연결) 된다. 
2. **인스턴스 초기화 -** this에 바인딩되어 있는 인스턴스를 초기화한다.
3. **인스턴스 반환 -** 생성자 함수 내부의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 `this`가 암묵적으로 반환된다.
    - 만약, `this`가 아닌 다른 객체를 명시적으로 반환하면 `this`가 아니라 return 문에 명시한 객체가 반환된다.
    - 하지만, 명시적으로 원시 값을 반환하면 원시 값은 무시되고 `this`가 반환된다.

```jsx
function Circle(radius) {
  // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.

  // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };

  // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다
}

// 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this를 반환한다.
const circle = new Circle(1);
console.log(circle); // Circle {radius: 1, getDiameter: ƒ}
```

**17.2.4 내부 메서드 [[Call]]과 [[Construct]]**

- 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드는 물론 함수로서 동작하기 위해 함수 객체만을 위한 [[Environment]], [[FormalParameters]]등의 내부 슬롯 과 [[Call]]. [[Construct]] 같은 내부 메서드를 추가로 가지고 있다.
- 함수가 일반 함수로서 호출되면 함수 객체의 내부 메서드 `[[Call]]`이 호출된다.
- new 연산자와 함께 생성자 함수로서 호출되면 내부 메서드 `[[Construct]]`가 호출된다.
- 모든 함수 객체는는 내부 메서드 `[[Call]]`를 가지고 있지만 모든 함수 객체가 `[[Construct]]`를 갖는 것은 아니다.

**17.2.5 constructor와 non-constructor의 구분**

- constructor(생성자 함수로서 호출 가능한 함수) - 함수 선언문, 함수 표현식, 클래스(클래스도 함수다)
- non-constructor(생성자 함수로서 호출할 수 없는 함수) - 메서드(ES6 메서드 축약 표현), 화살표 함수

**17.2.6 new 연산자**

- new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.
- new 연산자없이 일반적인 함수로서 호출하면 `this`는 전역 객체 window를 가리킨다.

**17.2.7 new.target**

- 생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해 ES6에서는 `new.target`을 지원한다.
- 함수 내부에서 `new.target`을 사용하면 new 연산자와 함께 생성자 함수로서 호출되었는지 확인할 수 있다.
    - new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 `new.target`은 함수 자신을 가리킨다. new 연산자 없이 일반 함수로서 호출된 함수 내부의 `new.target`은 undefined다.

```jsx
// 생성자 함수
function Circle(radius) {
  // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
  if (!new.target) {
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
const circle = Circle(5);
console.log(circle.getDiameter());  // 10
```

 ****