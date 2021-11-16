# Hook
> Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수이다.
> 

**Hook은 class를 작성하지 않고도 state와 다른 React의 기능들을 사용할 수 있게 해준다.** class형식으로 작성하려면 this키워드가 어떻게 작동하는지를 알아야 한다. JavaScript의 this키워드는 대부분의 다른 언어에서와는 다르게 작동함으로 사용자에게 큰 혼란을 주며, 코드의 재사용성과 구성을 매우 어렵게 만들고는 했다. 함수형에 가까운 Hook을 사용하면 보다 쉽게 코드를 작성할 수 있다. 

**Hook은 계층의 변화 없이 상태 관련 로직을 재사용할 수 있도록 도와준다.**

**Hook을 통해 서로 비슷한 것을 하는 작은 함수의 묶음으로 컴포넌트를 나누는 방법을 사용할 수 있다.** (구독 설정 및 데이터를 불러오는 것과 같은 로직) 또한 이러한 로직의 추적을 쉽게 할 수 있도록 리듀서를 활용해 컴포넌트의 지역 상태 값을 관리하도록 할 수 있다.

# 사용 규칙

- **최상위**(at the top level)에서만 Hook을 호출해야 한다. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행시킬 수 없다.
- **React 함수 컴포넌트 혹은 custom hook** 내에서만 Hook을 호출해야 한다. 일반 JavaScript 함수에서는 Hook을 호출해서는 안 된다.

# 참고

[https://ko.reactjs.org/docs/hooks-intro.html#motivation](https://ko.reactjs.org/docs/hooks-intro.html#motivation)

[https://ko.reactjs.org/docs/hooks-overview.html](https://ko.reactjs.org/docs/hooks-overview.html)
