# for of

```jsx
for (variable of iterable) {
statement
}
```

반복가능한 객체 (Array, Map, Set, String, TypedArray, arguments 객체 등을 포함)에 대해서 반복한다. 컬렉션 전용.

```jsx
const a = ['a', 'b', 'c'];

for (const [index, element] of a.entries())
  console.log(index, element);

// 0 'a'
// 1 'b'
// 2 'c'
```

인덱스를 구하기 위해서는 entries() 메서드를 사용해야 한다.

중간에 break 문을 만나면 반복문을 중단한다.



# forEach

```jsx
arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])
```

주어진 callback을 배열에 있는 각 요소에 대해 오름차순으로 한 번씩 실행한다.

callback 함수에서 값, 인덱스, 배열에 접근할 수 있다(for문보다 인덱스 값 접근이 편리).

 

```jsx
var arr = [1,2,3,4,5];
var newArr = arr.forEach(function(e, i) {
  return e;
});
// undefined
```

forEach()는 호출하는 배열을 변경할 수 있다.

값을 return할 수 없다. return해야 하는 경우 map을 사용해야 한다.

중간에 ```break```문을 사용할 수 없다. break가 필요한 경우 for문을 실행해야 한다.


# map

```jsx
arr.map(callback(currentValue[, index[, array]])[, thisArg])
```

배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 ```새로운 배열을 반환```한다.

기존의 배열을 이용해, 새로운 배열을 생성할 때 사용한다.

중간에 ```break``` 문을 사용할 수 없다. break가 필요한 경우 for문을 실행해야 한다.



# 참조

[for...of - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)

[Array.prototype.forEach() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

[Array.prototype.map() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
