### 프로토타입 활용 예시

---

```javascript
Set.prototype.union = function (set) {
  //합집합
  return new Set([...this, ...set]);
};
Set.prototype.intersection = function (set) {
  //교집합
  return new Set([...this].filter((item) => [...set].includes(item)));
};
Set.prototype.difference = function (set) {
  //차집합
  return new Set([...this].filter((item) => ![...set].includes(item)));
};
const set1 = new Set([1, 2, 3, 4]);
const set2 = new Set([3, 4, 5, 6]);

console.log(set1.intersection(set2));
console.log(set1.union(set2));
console.log(set1.difference(set2));
```
