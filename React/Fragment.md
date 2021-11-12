React문법에 의해 무조건 하나의 root를 가져야 한다. `<div>`태그로 감쌀 수 있으나 이를 반복하다보면 의미없는 태그들이 많아지게 된다. 이를 해결하기 위한 방법을 알아보자

# Component

컴포넌트를 만들어 이로 감싸면 필요없는 태그 없이 사용이 가능하다. 하지만 이와 동일한 작업을 하는 Fragment가 React에 구현되어 있음으로 이를 사용하는 것이 더 편하다.

```jsx
const Cover = (props) => return props.children
export default Cover;
```

```jsx
import Cover from './Cover'

const Hello = () => {
	<Cover>
		<div>Hello</div>
		<div>World</div>
	</Cover>
}
```

# Fragment

```jsx
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
```

# Empty Tag

<React.Fragment>를 줄여 빈 태그를 사용해도 된다. 단 축약형은 key값을 가지지 못한다.

```jsx
class Columns extends React.Component {
  render() {
    return (
      <>
        <td>Hello</td>
        <td>World</td>
      </>
    );
  }
}
```
