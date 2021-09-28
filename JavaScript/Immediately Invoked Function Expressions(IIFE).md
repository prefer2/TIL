## Immediately Invoked Function Expressions(IIFE)

```jsx
( function() {console.log('This will never run again');})();

// arrow function
( () => cosole.log('This will nver run again');
```

정의와 동시에 딱 한번만 실행할 수 있게 해주는 구문. 

()로 묶어 '함수 선언식'이 아닌 '**함수 표현식**'이라는 것을 명시적으로 알려주는 것.

함수 속의 것들은 함수 밖에서 접근 불가능. closure에 의해 private변수를 생성. private & encapsulated

하지만 ES6에서는 이럴 필요 없이 block속에서 const나 let을 사용하면 된다. 
