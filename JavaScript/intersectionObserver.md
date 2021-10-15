# 페이지 이동을 감지하기 위한 방법
## old way (Bad way)
scroll event를 계속해서 확인하며 현재 페이지 위치를 확인하는 방법. scroll 이벤트는 수천번, 수만번 일어날 수 있고 동적으로 일어나기 때문에 main thread에 영향을 줄 수 있다.


```jsx
const box = document.querySelector('.box').getBoundingClientRect();
window.addEventListener('scroll', function() {
  if(window.scrollY > box.top){
    nav.classList.add('get-bigger');
  }
  else {
    nav.classList.remove('get-bigger');
  }
})
```

## Intersection Observer API

> Intersection Observer API는 타겟 엘리먼트가 조상 엘리먼트, 또는 최상위 문서의 뷰포트(브라우저에서는 보통 브라우저의 viewport)의 교차영역에서 발생하는 변화를 비동기로 관찰하는 방법을 제공합니다.

다음과 같은 상황에서 사용하기 유용하다.
- 페이지가 스크롤 되는 도중에 발생하는 이미지나 다른 컨텐츠의 지연 로딩.
- 스크롤 시에, 더 많은 컨텐츠가 로드 및 렌더링되어 사용자가 페이지를 이동하지 않아도 되게 하는 infinite-scroll 을 구현.
- 광고 수익을 계산하기 위한 용도로 광고의 가시성 보고.
- 사용자에게 결과가 표시되는 여부에 따라 작업이나 애니메이션을 수행할 지 여부를 결정.

```
const io = new IntersectionObserver(callback[, options])
```

### options
- root: 
  - default: null, 브라우저의 viewport. 
  - 교차 영역의 기준이 될 root 엘리먼트. observe의 대상으로 등록할 엘리먼트는 반드시 root의 하위 엘리먼트여야 한다.
- rootMargin
  - default: '0px 0px 0px 0px'
  - root 엘리먼트의 마진값. css에서 margin을 사용하는 방법으로 선언할 수 있고, 축약도 가능하다. px과 %로 표현할 수 있다. rootMargin 값에 따라 교차 영역이 확장 또는 축소된다.
- threshold
  - default: 0
  - 0.0부터 1.0 사이의 숫자 혹은 이 숫자들로 이루어진 배열로, 타겟 엘리먼트에 대한 교차 영역 비율을 의미. 0.0의 경우 타겟 엘리먼트가 교차영역에 진입했을 시점에 observer를 실행하는 것을 의미하고, 1.0의 경우 타켓 엘리먼트 전체가 교차영역에 들어왔을 때 observer를 실행하는 것을 의미한다.



```jsx
const io = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.intersectionRatio > 0) {
      entry.target.classList.add('get-bigger');
    }
    else {
      entry.target.classList.remove('get-bigger');
    }
  })
})

const box = document.querySelector('.box');
io.observe(box);
```

# 참조
https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API


http://blog.hyeyoonjung.com/2019/01/09/intersectionobserver-tutorial/
