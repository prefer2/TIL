# state

리액트에서 state는 컴포넌트 내부에서 바뀔 수 있는 값을 의미한다. `props`는 (함수 매개변수처럼) **컴포넌트에 전달**되는 반면 `state`는 (함수 내에 선언된 변수처럼) **컴포넌트 안에서 관리된다**. 

props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값이며, 컴포넌트 자신은 해당 props를 **읽기 전용**으로만 사용할 수 있다. 따라서 props를 바꾸려면 부모 컴포넌트에서 바꾸어 주어야 한다. props와 state를 구분하는 이유는 **사용하는 쪽과 구현하는 쪽을 철저하게 분리시켜서 양쪽의 편의성을 각자 도모하기 위해서이다.**

# useState

useState 함수의 인자에는 상태의 초깃값을 넣어 준다. 초기값은 숫자, 문자열, 배열 등 형태는 자유롭다. state는 항상 초기값을 가진다.

useState는 state 변수, 해당 변수를 갱신할 수 있는 함수 이 두 가지 쌍을 반환한다. 이를 편리하게 사용하기 위해서 구조분해를 주로 사용한다. 함수의 이름을 꼭 set[state 변수]로 지정하지 않아도 되지만 주로 이와 같은 형식으로 사용한다.

```jsx
import React, { useState } from 'react';

function Example() {
  // 새로운 state 변수를 선언하고, count라 부르겠습니다.
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

위 예제에서는 useState를 사용하여 count의 초기 값을 0으로 지정하였다. 이후 버튼이 클릭 될 때마다 setCount함수가 호출되어 state 변수를 갱신한다.

# 참고

[https://ko.reactjs.org/docs/hooks-state.html](https://ko.reactjs.org/docs/hooks-state.html)
