# 11장 원시 값과 객체의 비교

### 📌 이것만은 꼭! **원시 타입과 객체 타입의 3가지 차이점**

<table>
  <tr>
    <td style="text-align:center">구분</td>
    <td style="text-align:center">원시 값</td>
    <td style="text-align:center">객체</td>
  </tr>
  <tr>
    <td style="text-align:center">값의 변경 가능 여부</td>
    <td style="text-align:center">변경 불가능</td>
    <td style="text-align:center">변경 가능</td>
  </tr>
  <tr>
    <td style="text-align:center">변수에 할당 시 저장되는 값</td>
    <td style="text-align:center">실제 값 </td>
    <td style="text-align:center">참조 값</td>
  </tr>
  <tr>
    <td rowspan="5">다른 변수에 할당할 때 <br /> 무엇이 어떻게 전달되는가</td>
    <td colspan="2" style="text-align:center">식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사해서 전달한다.</td>
  </tr>
  <tr>
    <td colspan="2" style="text-align:center">전달되는 메모리 주소를 통해 해당 메모리 공간의 원시 값 또는 참조 값을 참조한다. <br /> 공유에 의한 전달 (by sharing) </td>
  </tr>
  <tr>
    <td style="text-align:center">원시 값이 복사되어 전달</td>
    <td style="text-align:center">원본의 참조 값이 복사되어 전달</td>
  </tr>
    </tr>
    <td style="text-align:center">값에 의한 전달 (pass by value)</td>
    <td style="text-align:center">참조에 의한 전달 (pass by reference)</td>
  </tr>
</table>

### 📌 변경 불가능한 값, 변경 가능한 값, 변수, 상수 구분하기

- 변수: 하나의 값을 저장하기 위해 확보한 메모리 공간 자체, 그 메모리 공간을 식별하기 위해 붙인 이름
  - let 키워드로 선언한 변수는 재할당을 통해 참조하는 값을 바꿀 수 있다.
  - const 키워드로 선언한 상수는 값의 재할당이 금지된다. 단 한번만 값을 할당할 수 있다.
- 값: 변수에 저장되는 데이터 자체 (표현식의 평가 결과)
  - 원시 값은 변경할 수 없다.
  - 객체는 변경할 수 있다.

<br />

## 1. 원시 값 (Primitive type)

- 변경 불가능한 값 (immutable value)
- 읽기 전용 값 (read only)

### 변경 불가능한 값

![image](https://user-images.githubusercontent.com/76567238/207576990-9a160d7d-b45a-4444-8f35-a8c69ae9b214.png)

#### 불변성(immutability)

원시 값을 할당한 변수에 새로운 원시 값을 재할당하는 경우 변수가 참조하는 **메모리 공간의 주소**가 변경된다.

- 이전의 원시 값은 그대로
- 새로운 원시 값을 새로운 메모리 공간에 저장
- 변수는 새롭게 재할당한 원시 값을 참조

#### 문자열의 불변성

문자열은 원시 값으로 변경 불가능하다.

```js
var str = 'string';
str[0] = 'S';

console.log(str); // string
```

- 문자열: 0개 이상의 문자로 이뤄진 집합
  - 1개의 문자가 차지하는 메모리 공간의 크기: 2바이트
- 문자열은 유사 배열 객체로 인덱스를 사용해 각 문자에 접근할 수 있다.
- 하지만 문자열은 원시값이므로 변경할 수 없다.

### 값에 의한 전달

- 원시 값을 갖는 변수를 할당하면 해당 원시 값이 복사되어 전달된다.
- 원시 값은 서로 다른 메모리 공간에 저장된 별개의 값이다.
- 한쪽 값이 변경돼도 영향을 받지 않는다(서로 간섭할 수 없다).

#### 1. 다른 메모리 공간에 별개의 값으로 저장하는 방식

![image](https://velog.velcdn.com/images/narcoker/post/747b34a2-70b4-4f0f-840e-887cbc1ae9fe/image.png)

#### 2. 어느 한쪽의 변수에 재할당이 이뤄졌을 때 새로운 메모리 공간에 재할당된 값을 저장하는 방식

![image](https://velog.velcdn.com/images/narcoker/post/be6efe1b-5e4c-4257-82e8-86c9aab0fdbc/image.png)

<br />

## 2. 객체

### 자바스크립트의 객체 관리 방식

- Property key를 index로 하는 해시 테이블
- 클래스 없이 객체를 생성할 수 있다.
- 객체 생성 이후 동적으로 Property와 method를 추가할 수 있다.

### 변경 가능한 값

```js
var person = {
  name: 'lee',
};
```

![image](https://velog.velcdn.com/images/narcoker/post/c00c3c70-5ce2-4459-9f19-0c22eead7f27/image.png)

- 생성된 객체가 실제로 저장된 메모리 공간의 주소인 **참조 값**을 저장한다. (ex. 0x00001332)
  - 변수 `person`은 객체 `{name: 'Lee'}`를 가리킨다(참조한다).

```js
var person = {
  name: 'Lee',
};

person.name = 'Kim';
person.address = 'Seoul';

console.log(person); // {name: "Kim", address: "Seoul"}
```

- 재할당 없이 객체를 직접 변경할 수 있다.
  - 프로퍼티를 동적으로 생성할 수 있다.
  - 프로퍼티 값을 갱신할 수 있다.
  - 프로퍼티 자체를 삭제할 수 있다.

![image](https://velog.velcdn.com/images/narcoker/post/5bca99ee-0586-4f4e-b9ef-35ebd214c2a0/image.png)

- 객체를 할당한 변수 person의 참조 값은 변경되지 않는다.

### 참조에 의한 전달

- 객체를 참조하는 변수를 할당하면 원본의 참조 값이 복사되어 전달된다.
- 여러 개의 식별자가 하나의 객체를 공유할 수 있다.
- 원본 또는 사본 중 한쪽에서 객체를 변경하면 서로 영향을 주고받는다.

#### 예제 11-17

```js
var person = {
  name: 'Lee',
};
var copy = person;
console.log(copy === person); // true

copy.name = 'Kim';
person.address = 'Seoul';

console.log(person); // {name: "Kim", address: "Seoul"}
console.log(copy); // {name: "Kim", address: "Seoul"}
```

- copy와 person은 동일한 참조값을 갖는다. 즉, copy와 person은 동일한 객체를 참조한다.
- copy 또는 person 둘 중 한쪽에서 객체를 변경하면 서로 영향을 주고 받는다.

#### 예제 11-18

```js
var person1 = {
  name: 'Lee',
};

var person2 = {
  name: 'Lee',
};

console.log(person1 === person2); // false
console.log(person1.name === person2.name); // true
```

- 객체를 할당한 변수 `person1`과 `person2`를 비교하면 참조 값을 비교한다.
  - 각각 다른 메모리에 저장된 별개의 객체로 참조 값이 다르다.
- 원시 값을 할당한 변수 `name`을 비교하면 원시 값을 비교한다.
  - 평가 결과인 'Lee'라는 원시 값으로 같다.
