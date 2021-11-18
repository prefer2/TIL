# useEffect
**Effect Hook**을 사용하면 함수 컴포넌트에서 **side effect를 수행**할 수 있다. 화면에 렌더링된 이후에 비동기로 처리되어야 하는 부수적인 효과들을 흔히 side effect라고 일컽는다. 데이터 가져오기, 구독(subscription) 설정하기, 수동으로 React 컴포넌트의 DOM을 수정하는 것까지 이 모든 것이 side effects이다. 대표적으로 외부 API를 가져와 화면에 렌더링할 수 있는 것은 먼저 렌더링하고 실제 데이터는 비동기로 가져오는 것이 있다. 

useEffect는 리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook이다. React는 우리가 넘긴 함수를 기억했다가(이 함수를 `effect`라고 부른다) DOM 업데이트를 수행한 이후에 이 함수를 불러낸다.

useEffect는 기본적으로 렌더링되고 난 직후마다 실행된다. 첫번째 렌더링과 이후의 모든 업데이트에서 수행이 된다. 자바스크립트의 특성에 따라 리렌더링 될 때마다 다른 effect가 전달된다. 이러한 방식은 업데이트 로직을 빼먹으면서 발생할 수 있는 버그를 예방하며 일관성을 유지해준다. 

두 번째 파라미터 배열(dependencies)는 실행되는 조건을 의미한다.

```jsx
useEffect(()=>{...}, [dependencies])
```

## Clean Up

컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect에서 뒷정리(cleanup) 함수를 반환해 주어야 한다. effect가 함수를 반환하면 React는 그 함수를 정리(cleanup)가 필요한 때에 실행시킨다.

```jsx
useEffect(() => {
    console.log('effect');
    console.log(name);
    return () => {
      console.log('cleanup');
      console.log(name);
    };
  });
```

렌더링될 때마다 Clean Up 함수가 계속 나타나는 것을 확인할 수 있다. 그리고 Clean Up 함수가 호출될 때는 업데이트되기 직전의 값을 보여 준다.
