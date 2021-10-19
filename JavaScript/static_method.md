# 정적 메서드(static method)

```jsx
class User {
  static staticMethod() {
    console.log('this is static method');
  }
}

User.staticMethod();
```

`정적 메서드(static method)`는 프로토타입이 아닌 클래스 함수 자체에 설정하는 메서드이다. 클래스 함수를 위한 메스드이다. 정적 메서드는 어떤 특정한 객체가 아닌 클래스에 속한 함수를 구현하고자 할 때 주로 사용된다(보통 유틸리티 함수를 만드는데 사용된다).

클래스의 constructor(생성자)에 접근하지 않고 바로 정적 메서드를 실행하기 때문에 인스턴스를 생성하지 않고 클래스 내부에 바로 접근하여 실행 가능하다(static method만 있는 클래스인 경우엔 constructor 생략이 가능하다).
