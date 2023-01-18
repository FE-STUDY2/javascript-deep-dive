## 기본 this

전역 객체 (브라우저: window, nodeJS: global)

```javascript
//debugger;

const value = 1;

const obj = {
  value: 100,
  fn: function() {
    console.log("fn this: ",  this);
    console.log("fn this.value: ",  this.value);
    
    function fnInSide() {
      console.log("inside_fn this: ",  this);
      console.log("inside_fn this.value: ", this.value);  
    }
    fnInSide();
  }
};

obj.fn();
```

## 화살표 함수 this

상위 스코프의 this

```javascript
const value = 1;

const obj = {
  value: 100,
  arrowFn() {
    // 화살표 함수 내부의 this는 상위 스코프의 this를 가리킨다.
    setTimeout(() => console.log(this.value), 100);
  }
};

//debugger;

obj.arrowFn();
```

## callback 함수 this

전역 객체

```javascript
const value = 1;

const obj = {
  value: 100,
  fn: function() {
    setTimeout(function() {
      console.log("callback's this: ",  this);
      console.log("callback's this.value: ",  this.value);
      //debugger;
    }, 100);
  }
};

obj.fn();
```

## this binding

bind, apply, call

```javascript
const displayThis = function (key, value) {
  console.dir(this);
  console.log("key",key);
  console.log("value", value);
};

//debugger;

displayThis();

const obj = { displayThis };
obj.displayThis();

const bindingObject = { name: 'binding' };
displayThis.call(bindingObject, 'language', 'javascript');
displayThis.apply(bindingObject, ['language', 'typescript']);
displayThis.bind(bindingObject)();
```

## 생성자 함수 this

- new 키워드 없을 경우 일반 함수처럼 동작하고 리턴이 없을 경우 undefined반환
- new 키워드 있을 경우 this를 해당 object로 binding해주고 리턴을 명시하지 않아도 암묵적으로 (해당 object) this를 반환

```javascript
//debugger

const me = Person('Lee', 23);

console.log(me);
console.log({name: window.name, age: window.age});

const itsMe = new Person('Kim', 19);

console.log(itsMe);
console.log({name: window.name, age: window.age});
console.log({name: itsMe.name, age: itsMe.age});

function Person(name, age) {
  this.name = name;
  this.age = age;
};
```

## 2차과제예시 활용해본 예시

올바른 활용방법이라고 하기는 무리가 있을 것 같으나 해당 방식으로도 활용해도 에러 없이 잘 동작함을 공유하고 싶어서 작성해 봄

```javascript
debugger;

const resultTime = parseKoreaTime.call('123 min');

console.log(resultTime);

function parseKoreaTime() {
  const timeRegExp = /[0-9]+(?= min)/;
  const [stringOfMimute] = timeRegExp.exec(this);

  const time = Number(stringOfMimute);
  const hour = Math.floor(time / 60);
  const mimute = time - hour * 60;
    
  return `${hour ? `${hour}시간 ` : ""}${mimute}분`;
}
```

