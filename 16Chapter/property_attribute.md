# 프로퍼티 어트리뷰트

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

- 프로퍼티 어트리뷰트 : 자바스크립트 엔진은 프로퍼티를 생성할 때 **프로퍼티의 상태**를 나타내는 것 
  - 프로퍼티의 상태 : 프로퍼티의 값(Vaule), 값의 갱신 가능 여부(writable),  
                    열거 가능 여부(enumerable), 재정의 가능 여부(configurable) 말한다.
- 자바스크립트 엔진이 관리하는 내부 상태 값인 내부 슬롯이다.

```js
const person = {
  name: 'Kim'
}

console.log(Object.getOwnPropertyDescriptor(person, 'name'))
//{value: 'Kim', wirtable: true, enumerable:true, configurable: true}
```

- 프로퍼티 어트리뷰트는 내부 슬롯이므로, 직접 접근할 수 없지만 위에 예제에 
  사용된 **Object.getOwnPropertyDescriptor()메소드를 사용하여 간접적으로 확인 가능**하다 

- 프로퍼티 디스크립터 객체 : Object.getOwnPropertyDescriptor() 메소드를 사용할때 
                              **프로퍼티의 정보를 제공 객체를 반환**
                          위에 예제에서 // 주석으로 단 출력 값이 해당 객체이다.

## 데이터 프로퍼티와 접근자 프로퍼티 

- 프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분 

  - 데이터 프로퍼티(Data Property) : 키(Key)와 값(Value) 구성.

  - 데이터 프로퍼티의 프로퍼티 어트리뷰트
    
    - 자바스크립트 엔진이 프로퍼티를 생성할 때 자동으로 생성

   |프로퍼티 어트리뷰트| 프로퍼티 디스트립터 객체의 프로퍼티|설명|
   |------------------|---------------------------------|---|
   |'\[''\[\'Value'\]'\']\'|value| - 프로퍼티 키를 통해 프로퍼티 값에 접근하면 반환되는 값이다.|
                                   - 프로퍼티 키를 통해 프로퍼티 값을 변경 하면 '\[''\[\'Value'\]'\']\'에
                                     갑을 재할당한다. 이때 프로퍼티가 없으면 프로퍼티를 동적으로 생성하고 
                                     생성된 프로퍼티의 '\[''\[\'Value'\]'\']\'에 값을 저장
   |'\[''\[\'Writable'\]'\']\'|writable| - 프로퍼티 값의 변경 가능 여부를 불리언 값을 갖는다|            
                                         - '\[''\[\'Writable'\]'\']\'값이 false인 경우 해당 프로퍼티의 
                                           '\[''\[\'Value'\]'\']\'의 값을 변경할 수 없는 읽기 전용 프로퍼티가 된다.
   |'\[''\[\'Enumerable'\]'\']\'|enumerable| - 프로퍼티의 열거 가능여부를 불리언 값으로 갖는다.|
                                             - '\[''\[\'Enumerable'\]'\']\'의 값이 false인 경우 프로퍼티는 
                                               for...in문이나 Object.keys 메서드 등 열거할 수 없다.
   |'\[''\[\'Configurable'\]'\']\'|configurable| - 프로퍼티의 재정의 가능 여부를 나타내며 불리언 값을 갖는다.|
                                                 - '\[''\[\'Configurable'\]'\']\'의 값이 false 경우 해당   프로퍼티 삭제, 프로퍼티 어트리뷰트 값의 변경이 금지 된다.
                                                 단, '\[''\[\'Writable'\]'\']\'이 true인 경우 '\[''\[\'Value'\]'\']\'의 변경과 '\[''\[\'Writable'\]'\']\'을
                                                 false로 변경하는 것을 허용한다.

```js
const person = {
  name: 'Kim'
}

person.age = 30;

console.log(Object.getOwnPropertyDescriptor(person))
//{value: 'Kim', wirtable: true, enumerable:true, configurable: true}
//{value: 30, wirtable: true, enumerable:true, configurable: true}
```
위에 예시처럼 프로퍼티가 생성 될 때 '\[''\[\'Value'\]'\']\'의 값이 초기화 되며, '\[''\[\'Writable'\]'\']\','\[''\[\'Enumerable'\]'\']\', '\[''\[\'Configurable'\]'\']\'의 값은 true로 초기화 된다. 이것은 프로퍼티를 동적으로 추가해도 마찬가지이다. 



  - 접근자 프로퍼티(Accessor Property) : 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나,
                                       저장할때 호출되는 접근자 함수(Accessor Function)로 구성.
    -접근자 함수는 getter/ setter 함수라고 부른다.

- 접근자 프로퍼티의 프로퍼티 어트리뷰트
    
    

   |프로퍼티 어트리뷰트| 프로퍼티 디스트립터 객체의 프로퍼티|설명|
   |------------------|---------------------------------|---|
   |'\[''\[\'Get'\]'\']\'|get| - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자함수이다.|
                                 즉, 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트리뷰트 '\[''\[\'Get'\]'\']\'의 값, 즉 getter 함수가 호출되고 그결과 프로퍼티 값으로 반환된다.
   |'\[''\[\'Set'\]'\']\'|set| - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할때 호출되는 접근자 함수이다.|
                                 즉, 접근자 프로퍼티 키로 프로퍼티 값을 저장하면 프로퍼티 어트리뷰트 '\[''\[\'Set'\]'\']\'의 값, 즉 setter 함수가 호출되고 그결과가 프로퍼티 값으로 반환된다.
   |'\[''\[\'Enumerable'\]'\']\'|enumerable| 데이터 프로퍼티의 '\[''\[\'Enumerable'\]'\']\'과 같다.|
                                             
   |'\[''\[\'Configurable'\]'\']\'|configurable| - 데이터 프로퍼티의 '\[''\[\'Configurable'\]'\']\'과 같다.|
                                               
```js
const person = {
  firstName: 'seon-mi',
  lastName: 'kim',
 
  get fullName() {
    return `${this.firstName} ${this.lastName}`
  },

  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ')
  }
}

console.log(person.firstName + ' ' + person.lastName)


person.fullName ='in-hyuk Bea'

console.log(person)
console.log(person.fullName)

let descriptor = Object.getOwnPropertyDescriptor(person, 'fullName')
console.log(descriptor)

descriptor = Object.getOwnPropertyDescriptor(person, 'fullName')
console.log(descriptor)
//{get: f, set: f, enumerable: true, configurable: ture}
```

위에 예시 통해 접근자 프로퍼티는 자체적으로 값을 가지지 않으며 다만 데이터 프로퍼티의 값을 읽거나 저장할때 관여할 뿐이다. 

- 내부 슬롯/메서드 관점에서 설명하자면

1. 프로퍼티 키가 유효한지 확인. 
  - 프로퍼티 키는 문자열 또는 심벌이여야한다. 예제에서 프로퍼티 키  "fullName"은 문자열이므로 유효한 프로퍼티 키이다. 
2. 프로토타입 체인에서 프로퍼티를 검색한다. 
   - person 객체에 fullName 프로퍼티가 존재한다. 
3. 검색된 fullName 프로퍼티가 데이터 프로퍼티인지 접근자 프로퍼티인지 확인 
   - fullName 프로퍼티는 접근자 프로퍼티이다. 
4. 접근자 프로퍼티 fullName의 프로퍼티 어트리뷰트 '\[''\[\'Get'\]'\']\'의 값, 즉 getter 함수를 호출 하여 그결과를 반환한다.
   - 프로퍼티 fullName의 프로퍼티 어트리뷰트 '\[''\[\'Get'\]'\']\'의 값이 getOwnPropertyDescriptor() 메소드가 반환하는 
     프로퍼티 디스크립터 객체의 get 프로퍼티 값과 같다. 

- 프로토타입(prototype)

  - 프로토타입 : 어떤 객체의 상위객체의 역할을 하는 객체다.
    - 하위 객체에게 자신의 프로퍼티와 메소드를 상속
     - 하위 객체는 상위 객체로 상속 받은 프로퍼티와 메소드를 자신의 프로퍼티 또는 메소드처럼 자유롭게 사용가능
    
    - 프로토타입 체인 : 프로토타입이 단방향 링크드 리스트 형태로 연결되어 있는 상속 구조
     - 객체의 프로퍼티나 메소드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메소드가 없다면 
       프로토타입 체인을 따라 프로토타입의 프로퍼티나 메서드를 차례대로 검색   

### 접근자 프로퍼티와 데이터 프로퍼티 구별 

```js
Object.getOwnPropertyDescriptor(Object.prototype, '__proto__')
//{get: f, set: f, enumerable: false, configurable: true}

Object.getOwnPropertyDescriptor(function() {}, 'prototype')
//{value: {...}, writable: true, enumerable: false, configurable: false}
```

위에 예제를 보면 Object.getOwnPropertyDescriptor()메소드로 반환한 프로퍼티 어트리뷰트를 객체로 표현한 프로퍼티 디스크립터 객체의 프로퍼티가 다른것을 알수 있다. 


## 프로퍼티의 정의 

- 프로퍼티의 정의 : 새로운 프로퍼티를 추가하면 프로퍼티 어트리뷰트를 명시적으로 정의 하거나 기존 프로퍼티의 프로퍼티 어트리뷰트를 제정의 하는 것을 말한다. 
  - Object.defineProperty 메소드를 사용하면 프로퍼티의 어트리뷰트를 정의 가능
     - 인수로는 객체의 참조와 데이터 프로퍼티의 키인 문자열과 디스크립터 객체를 전달 
     - 위에 메소드로 프로퍼티을 정의 할 때 프로퍼티 디스크립터 객체의 프로퍼티를 일부 생략 가능
     - 위에 메소드는 한번에 하나의 프로퍼티만 정의 가능, 여러개 정의 하려면 Object.defineProperties 사용하면된다.     

```js
const person = {}
  
  //데이터 프로퍼티의 정의
  
  Object.defineProperty(person, 'firstName', {
    value: 'seon-mi',
    writable: true,
    enumerable: true,
    configurable: true
  })
  
  Object.defineProperty(person, 'lastName', {
    value: 'Kim',
  })
  
  let descriptor = Object.getOwnPropertyDescriptor(person, 'fristName')
  console.log('firstName', descriptor)
  //{value: 'seon-mi', wirtable: true, enumerable:true, configurable: true}

  descriptor = Object.getOwnPropertyDescriptor(person, 'lastName')
  console.log('lastName', descriptor)
    //{value: 'Kim', wirtable: false, enumerable:false, configurable: false}


 Object.defineProperty(person, 'fullName',{
  firstName: 'seon-mi',
  lastName: 'kim',
 
  get fullName() {
    return `${this.firstName} ${this.lastName}`
  },

  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ')
  },

  enumerable: true,
  configurable: true
})

 let descriptor = Object.getOwnPropertyDescriptor(person, 'fullName')
  console.log('fullName', descriptor)
  //{get: f, set: f, enumerable:true, configurable: true}
```

- 프로퍼티 디스크립트 객체에 생략된 어트리뷰트는 다음과 같이 기본값 적용 

| 프로퍼티 디스크립터 객체의 프로퍼티 | 대응하는 프로퍼티어트리뷰트 | 생략했을 때 기본 값 |
|----------------------------------|---------------------------|-------------------|
| value | '\[''\[\'Value'\]'\']\' | undefined |
| get | '\[''\[\'Get'\]'\']\' | undefined |
| set | '\[''\[\'Set'\]'\']\' | undefined |
| writable | '\[''\[\'Writable'\]'\']\' | false |
| enumerable | '\[''\[\'Enumerable'\]'\']\' | false |
| confugurable | '\[''\[\'Configurable'\]'\']\' | false |



## 객체 변경 방지 

- 객체는 변경 가능한 값이므로 재할당 없이 직접 변경 할 수 있다. 
  즉, 프로퍼티를 추가하거나 삭제, 값을 갱신 할수 있으며, Object.defineProperty, Object.defineProperties 통해 프로퍼티 어트리뷰트를 재정의 가능

 - 객체 변경 방지 메소드

| 구분 | 메소드 | 프로퍼티 추가 | 프로퍼티 삭제 | 프로퍼티 값 읽기 | 프로퍼티 값 쓰기 | 프로퍼티 어트리뷰트 재정의 |   
|------|--------|--------------|--------------|-----------------|-----------------|--------------------------|   
| 객체 확장 금지 | Object.PreventExtensions | X | O | O | O | O |   
| 객체 밀봉 | Object.seal | X | X | O | O | X |   
| 객체 동결 | Object.freeze | X | X | O | X | X |

### 객체 확장 금지 

- Object.PreventExtensions 메서드는 객체의 확장을 금지
 - 확장이 금지된 객체는 프로퍼티 추가가 금지됨 
 - 프로퍼티의 동적 추가와 Object.defineProperty 방법 금지
 - Object.isExtensible 메소드로 확장 가능한 객체인지 여부 확인 가능

 ```js
 const person = { name: 'Kim' }
 console.log(Object.isExtensible(person))
 //true
 
 Object.PreventExtensions(person)
 //객체 확장 금지 객체 
 console.log(Object.isExtensible(person))
 //false

 person.age = 30 // 무시. strict mode에서 에러발생
 console.log(person)
 //{ name:'Kim' }

 delete person.name // 삭제 가능
 console.log(person) // {}

 Object.defineProperty(person, 'age', { age: 30 })
 //TypeError: Cannot define property age, object is no extensible

 ```

 ### 객체 밀봉 

 - Object.seal 메소드로 객체 밀봉 
  - 프로퍼티 추가, 삭제, 어트리뷰트 재정의 금지 
  - 밀봉된 객체는 읽기와 쓰기만 가능하다
  - 밀봉된 객체인지 확인 여부 메소드 Object.isSealed 
  
```js
  const person = { name: 'Kim' }
  console.log(Object.isSealed(person)) //false
  //true
 
  Object.seal(person)
  //객체 밀봉 
  console.log(Object.isSealed(person))
  //true
 
  console.log(Object.getOwnPropertyDescriptors(person))
  // configurable: false
  
  person.age = 30 // 무시. strict mode에서 에러발생 프로퍼티 추가금지
  console.log(person)
  //{ name:'Kim' }

  delete person.name // 삭제 금지
  console.log(person) // {name:'Kim'}

  person.name ='Lee' //프로퍼티 값 갱신 가능 
  console.log(person) // {name: 'Lee'}
  
  //프로퍼티 어트리뷰트 재정의 금지 
  Object.defineProperty(person, 'name', { configurable: true })
  //TypeError: Cannot redefine property: name

```

### 객체 동결 

- Object.freeze 메소드는 객체를 동결
  - 프로퍼티 추가, 삭제 어트리뷰트 재정의, 값 갱신 금지
  - 동결된 객체는 읽기만 가능
  - 동결된 객체인지 확인하는 메소드 Object.isFrozen

```js
  const person = { name: 'Kim' }
  console.log(Object.isFrozen(person)) //false
  //true
 
  //객체 동결 
  Object.freeze(person)
  console.log(Object.isFrozen(person))
  //true
 
  console.log(Object.getOwnPropertyDescriptors(person))
  // writable ,configurable: false
  
  person.age = 30 // 무시. strict mode에서 에러발생 프로퍼티 추가금지
  console.log(person)
  //{ name:'Kim' }

  delete person.name // 삭제 금지
  console.log(person) // {name:'Kim'}

  person.name ='Lee' //프로퍼티 값 갱신 불가 
  console.log(person) // {name: 'Kim'}
  
  //프로퍼티 어트리뷰트 재정의 금지 
  Object.defineProperty(person, 'name', { configurable: true })
  //TypeError: Cannot redefine property: name
```

### 불변 객체 

- 위에 3개의 객체 변경 방지 메소드들은 얕은 변경 방지로 직속 프로퍼티만 변경 방지되고 중첩 객체까지는 영향을 주지 못함
 - Oject.freeze 메소드로 객체를 동결하여도 중첩 객체까지 동결 불가 

```js
  const person = {
     name: 'Kim',
     address: {city:'Seoul'} 
  }
  

  //직속 프로퍼티만 객체 동결 
  Object.freeze(person)
  console.log(Object.isFrozen(person))
  //true
  console.log(Object.isFrozen(person.address))
  //false 중접객체까지는 동결하지 못함

  
  person.age = 30 // 무시. strict mode에서 에러발생 프로퍼티 추가금지
  console.log(person)
  //{ name:'Kim' }

  person.address.city ='Busan'
  console.log(person)
  //{name:'Kim', address:{city:'Busan'}}
```
위와 같이 중첩객체는 동결하지 못한다. 

중첩 객체까지 동결하려면? 
- 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze 메소드를 사용

해당 예시 코드 


```js
function deepFreeze(target) {
  if(target && typeof target === 'object' && !Object.isFrozen(target)){
    Object.freeze(target)
    // 모든 프로퍼티를 순회하며 재귀적으로 동결 
    // Object.keys 메소드는 객체 자신의 열거 가능한 프로퍼티 키를 배열로 반환
    //foEach 메서드는 배열을 순회하며 각 요소에 대하여 콜백함수를 실행
    Object.keys(target).forEach(key => deepFreeze(target[key]))    
  }
  return target
}

const person = {
  name:'Kim',
  address:{city:'Seoul'}
}

deepFreeze(person)

console.log(Object.isFrozen(person)) //true

console.log(Object.isFrozen(person.address)) //true

person.address.city = 'Busan'
console.log(person) //{name:'Kim', address:{city:'Seoul'}}
```