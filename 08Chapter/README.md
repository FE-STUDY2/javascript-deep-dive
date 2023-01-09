## 08장 제어문

### 블록문
0개 이상의 문을 중괄호로 묶은 것

```jsx
// 블록문
{
  var foo = 10
}

// 제어문
var x = 1
if (x < 10) {
  x++
}

// 함수 선언문
function sum(a, b) {
  return a + b
}
```

### if else문
- 주어진 조건식의 평과 결과에 따라 블록문의 실행을 결정한다.
```jsx
if(조건식) {
  // 조건식이 참이면 이 코드 블록 실행
} else {
  // 조건식이 거짓이면 이 코드 블록 실행
}
```

### switch문
```jsx
switch(표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행될 문
    break;
  dafault:
    switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문
}
```

### for문
```jsx
for (변수 선언문,할당문; 조건식; 증감식;) {
	조건식이 참인 경우 반복 실행될 문
}

for (var i = 0; i < 2; i++) {
  console.log(i);
}
```

### while문
```jsx
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}
```

### break문
```jsx
foo: {
  console.log(1);
  break foo; // foo 레이블 블록문을 탈출한다.
  console.log(2);
}

console.log('Done!');
```

### continue문
```jsx
var string = 'Hello World.';
var search = 'l';
var count = 0;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// 참고로 String.prototype.match 메서드를 사용해도 같은 동작을 한다.
const regexp = new RegExp(search, 'g');
console.log(string.match(regexp).length); // 3
```
