# Component(컴포넌트)

컴포넌트는 독립적인 기능을 수행하는 단위 모듈을 의미한다. 리액트에서 컴포넌트는 앱을 이루는 최소한의 단위이다. 개념적으로 컴포넌트는 JavaScript 함수와 유사하다. “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다. 합성을 이용하여 “UI를 재사용할 수 있고 독립적인 단위로 쪼개어 생각”할 수 있게 한다.

### 함수형 컴포넌트

```js
import Reactfrom 'react';

functionReactFunc(props) {
  //...statements
}
```

### **클래스형 컴포넌트**

```js
import Reactfrom 'react';

classReactFuncextendsReact.Component {
  constructor(props){
    super(props)
    this.state = {}
  }

  render() {
    return (
    //...statements
    );
  }
}
```
