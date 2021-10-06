미들웨어(middleware)는 요청과 응답의 중간에 위치하여 미들웨어라고 불린다. 라우터, 에러 핸들러도 미들웨어이다. Express에서는 사실상 모든 것이 미들웨어이다. 

[공식 문서](https://expressjs.com/ko/guide/using-middleware.html)에 따르면 미들웨어는 애플리케이션의 **요청-응답 주기 중 req, res 객체에 대한 접근 권한을 갖고 변형시킬 수 있으며 미들웨어 스택 내 다음 미들웨어 함수에 next호출을 통해 접근할 수 있는 함수**이다. 이때 미들웨어 스택은 코드 순(위에서부터 아래)으로 쌓여 있다. 따라서 express에서는 코드의 순서가 중요하다.

Express 애플리케이션은 다음과 같은 유형의 미들웨어를 사용할 수 있다.

- [애플리케이션 레벨 미들웨어](https://expressjs.com/ko/guide/using-middleware.html#middleware.application)
- [라우터 레벨 미들웨어](https://expressjs.com/ko/guide/using-middleware.html#middleware.router)
- [오류 처리 미들웨어](https://expressjs.com/ko/guide/using-middleware.html#middleware.error-handling)
- [기본 제공 미들웨어](https://expressjs.com/ko/guide/using-middleware.html#middleware.built-in)
- [써드파티 미들웨어](https://expressjs.com/ko/guide/using-middleware.html#middleware.third-party)

## 예시

```jsx
app.use((req, res, next) => {
	console.log('미들웨어 실행');
	next();
}
```

app.use에 매개변수가 req, res, next인 함수를 넣으면 된다. 만약 next를 실행하지 않는다면 다음 미들웨어가 실행되지 않는다.

주소를 첫 번째 인수로 넣지 않는다면 미들웨어는 모든 요청에서 실행되고, 주소를 넣는다면 해당하는 요청에서만 실행된다.


| app.use(미들웨어)          | 모든 요청에서 미들웨어 실행                |
|----------------------------|--------------------------------------------|
| app.use('/abc', 미들웨어)  | abc로 시작하는 요청에서 미들웨어 실행      |
| app.post('/abc'. 미들웨어) | abc로 시작하는 POST 요청에서 미들웨어 실행 |


자주 사용하는 패키지인 [morgan의 코드](https://github.com/expressjs/morgan/blob/master/index.js)를 확인해보면 위와 같은 형식의 미들웨어로 구성되어 있는 것을 확인할 수 있다.
