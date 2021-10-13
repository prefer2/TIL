# 버튼 클릭 시 원하는 페이지로 부드럽게 이동하는 방법

## old version
```jsx
btnScrollTo.addEventListener('click', function(e) {
  
  const s1coords = section1.getBoundingClientRect();
  window.scroll({
  left: s1coords.left + window.scrollX, 
  top: s1coords.top + window.scrollY,
  behavior:'smooth'
  });
  
})
```
### getBoundingClientRect()

원하는 요소의 위치를 알 수 있다. viweport를 기준으로 하는 상대적인 값이기 때문에 스크롤을 하면(viewport가 바뀌면) 값이 바뀐다.


<img src="https://user-images.githubusercontent.com/67692759/137072584-7d1f9dca-17a6-4fbe-82f0-204f946845b4.png" width="500px">


### scrollX, scrollY, scroll

scrollX는 문서가 수평으로 얼마나 스크롤 되었는지를, scrollY는 문서가 수직으로 얼마나 스크롤 되었는지를 리턴해준다.
getBoundingClientRect()로 구한 값이 상대적인 값이기 때문에 절대적인 위치를 구하기 위해서는 scrollX와 scrollY를 더해주어야 한다. 

scroll는 지정된 위치로 스크롤 해준다. x-좌표는 문서의 왼쪽상단부터 시작하는 픽셀단위의 가로축, y-좌표는 문서의 왼쪽상단부터 시작하는 픽셀단위의 세로축이다. behavior를 설정하여 ```smooth```또는 ```instant```하게 스크롤 되도록 정할 수 있다.



## modern version
```jsx
btnScrollTo.addEventListener('click', function(e) {
  section1.scrollIntoView({behavior: 'smooth'})
})
```


# 참조
https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect
https://developer.mozilla.org/ko/docs/Web/API/Element/scrollIntoView
