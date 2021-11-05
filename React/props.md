# Props

props는 properties를 줄인 표현으로 컴포넌트 속성을 설정할 때 사용하는 요소이다. props 값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정할 수 있다. React에서 props는 Immutable Data(변하지 않는 데이터)이다(A component should manage its own state, but it should not manage its own props. `props` is essentially "state that is managed by the component owner." That's why props are *immutable*.).

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

export default Welcome;
```

```jsx
import React from 'react';
import Welcome from './Welcome';
 
const App = () => {
  return <MyComponent name="React" />;
};
 
export default App;
```

## Default값 설정

```jsx
import React from 'react';
 
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
 
Welcome.defaultProps = {
  name: '기본 값'
};
 
export default MyComponent;
```

## Children

리액트 컴포넌트를 사용할 때 컴포넌트 태그 사이의 내용을 보여 주는 props.

태그 사이의 값들을 모두 가져오기때문에 shell 컴포넌트를 만들때 사용하기 좋다.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.children}</h1>;
}

export default Welcome;
```

```jsx
import React from 'react';
import Welcome from './Welcome';
 
const App = () => {
  return <MyComponent>This is my Children</MyComponent>;
};
 
export default App;
```

## 구조분해(destructuring assignment)

```jsx
import React from 'react';

const Welcome = ({ name, age }) => {
  return (
  <>
    <h1>Hello, {name}</h1>
    <h1>I'm {age}</h1>
  </>
  );
};

MyComponent.defaultProps = {
  name: '기본 이름'
};

export default MyComponent;
```

# 참고

[https://stackoverflow.com/questions/47471131/why-are-react-props-immutable](https://stackoverflow.com/questions/47471131/why-are-react-props-immutable)

[https://ko.reactjs.org/docs/components-and-props.html](https://ko.reactjs.org/docs/components-and-props.html)
