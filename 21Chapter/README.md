## 21장 빌트인 객체 

```jsx
let foo = 123
console.log(window.foo)
```

```jsx
var x = 10

function foo() {
  y = 20
  console.log(x + y)
}

foo() 

console.log(window.x)
console.log(window.y)

delete x
delete y

console.log(window.x)
console.log(window.y)


```
