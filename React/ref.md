# Ref

ref는 HTML에서 id를 사용하여 이름을 다는 것처럼 React에서 DOM에 이름을 다는 방법이다. ref는 전역적으로 작동하지 않고 컴포넌트 내부에서만 작동한다. ref는 DOM을 직접적으로 건드려야 할 때만 사용한다.

- 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때.
- 애니메이션을 직접적으로 실행시킬 때.
- 서드 파티 DOM 라이브러리를 React와 같이 사용할 때.

# Ref 생성하기

## 콜백함수

```jsx
<input ref={(ref) => {this.input=ref}} />
```

ref를 달고자 하는 요소에 ref라는 콜백 함수를 props로 전달해 주면 된다. 이 콜백 함수는 ref 값을 파라미터로 전달받는다. 그리고 함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정해 준다.

input 요소는 앞으로 리액트 코드 내에서 **this.input**을 통하여 접근이 가능하다. 즉, 리액트 내에서 id 처럼 쓰이게 된 것이다. 

## createRef()

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```

Ref는 `React.createRef()`를 통해 생성되고 `ref` 어트리뷰트를 통해 React 엘리먼트에 부착된다. 보통, 컴포넌트의 인스턴스가 생성될 때 Ref를 프로퍼티로서 추가하고, 따라서 컴포넌트의 인스턴스의 어느 곳에서도 Ref에 접근할 수 있게된다.

```jsx
const node = this.myRef.current;
```

`render` 메서드 안에서 ref가 엘리먼트에게 전달되었을 때, 그 노드를 향한 참조는 ref의 `current` 어트리뷰트에 담겨 있다. ref를 설정해 준 DOM에 접근하려면 this.input.current를 조회하면 된다.

> *컴포넌트가 마운트될 때 React는 current 프로퍼티에 DOM 엘리먼트를 대입하고, 컴포넌트의 마운트가 해제될 때 current 프로퍼티를 다시 null로 돌려놓습니다. ref를 수정하는 작업은 componentDidMount 또는 componentDidUpdate 생명주기 메서드가 호출되기 전에 이루어집니다.*
> 

ref에 접근할 수 있는 시점은 React 노드가 실제로 DOM에 반영되는 시점부터이다. DOM이 유동적이기에 React는 객체를 반환해 current 프로퍼티의 값을 계속해서 수정한다.

# Why?

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      value: ""
    };
  }

  render() {
    return (
      <input
        value={this.state.value}
        onChange={({ target: { value } }) =>
          this.setState({ ...this.state, value })
        }
      />
    );
  }
}
```

다음과 같은 코드를 실행하면 input에 값을 입력할때마다 state가 변하게 되어 rerendering이 일어나게 된다. 이는 컴퓨터 자원을 소모하는 불필요한 프로세스이다.

```jsx
class Example2 extends React.Component {
  constructor(props) {
    super(props);

    this.ref = React.createRef();
  }

  render() {
    return (
      <input ref={this.ref} />
    );
  }
}
```

input은 state를 변경하지 않기에 불필요한 re-rendering은 일어나지 않는다. 

- refs make it easier to uniquely identify + select in linear time the corresponding element (as compared to id which multiple elements can, by mistake, have the same value for + compared to document.querySelector which needs to scan the DOM to select the correct element)
- refs are aware of react component lifecycle, so react would make sure that refs are updated to null when component unmounts and more out of the box convenience.
- refs as a concept + syntax are platform agnostic, so you can use the same understanding in react native and the browser, while query selector is a browser thing
- for SSR, where there is no DOM, refs can still be used to target react elements

# 참조

[https://ko.reactjs.org/docs/refs-and-the-dom.html#accessing-refs](https://ko.reactjs.org/docs/refs-and-the-dom.html#accessing-refs)

[https://tecoble.techcourse.co.kr/post/2021-05-15-react-ref/](https://tecoble.techcourse.co.kr/post/2021-05-15-react-ref/)

[https://stackoverflow.com/questions/59198952/using-document-queryselector-in-react-should-i-use-refs-instead-how](https://stackoverflow.com/questions/59198952/using-document-queryselector-in-react-should-i-use-refs-instead-how)
