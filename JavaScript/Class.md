# Class

> 모던 자바스크립트 Deep Drive를 읽으며 공부한 내용입니다
> 

# 클래스 정의

클래스는 class 키워드를 사용하여 정의한다. 클래스 이름은 파스칼 케이스를 사용하는 것이 일반적이다. 클래스 몸체에서 정의할 수 있는 메서드는 `constructor(생성자), 프로토타입 메서드, 정적 메서드` 세 가지가 있다.

```jsx
const Person = class MyClass {};
```

일반적이지는 않지만 함수와 마찬가지로 표현식으로도 클래스를 정의할 수 있다. 이는 클래스가 값으로 사용할 수 있는 일급 객체라는 것을 의미한다.

```
일급 객체의 특징
- 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
- 변수나 자료구조(객체, 배열)등에 저장할 수 있다.
- 함수의 매개변수에 전달할 수 있다.
- 함수의 반환값으로 사용할 수 있다.
```

더 자세히 알아보면 클래스는 함수다. 따라서 클래스는 값처럼 사용할 수 있는 일급 객체다. 클래스와 생성자 함수의 정의 방식을 비교해 보면 형태적인 면에서 매우 유사하다.

# 호이스팅

클래스 선언문으로 정의한 클래스는 함수 선언문과 같이 런타임 이전에 먼저 평가되어 함수 객체를 생성한다. 이때 클래스가 평가되어 생성된 함수 객체는 생성자 함수로서 호출할 수 있는 함수, 즉 constructor다. 단, 클래스는 클래스 이전에 참조할 수 없다.

클래스 선언문도 변수 선언, 함수 선언과 마찬가지로 호이스팅이 발생한다. 단, 클래스는 let, const 키워드로 선언한 변수처럼 호이스팅된다. 따라서 클래스 선언문 이전에 TDZ에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다.

# 인스턴스 생성

클래스는 생성자 함수이며 new 연산자와 함께 호출되어 인스턴스를 생성한다.

```jsx
class Person {}

const me = new Person();
```

# 메서드

## constructor

constructor는 `인스턴스를 생성하고 초기화`하기 위한 특수한 메서드다. constructor 내분의 this는 생성자 함수와 마찬가지로 클래스가 생성한 인스턴스를 가리킨다.

```jsx
class Person {
	constructor(name) {
		this.name = name;
	}
}
```

constructor는 별도의 반환문을 갖지 않아야 한다. new 연산자와 함께 클래스가 호출되면 생성자 함수와 동일하게 암묵적으로 this, 즉 인스턴스를 반환하기 때문이다. 

## 프로토타입 메서드

```jsx
class Person {
	constructor(name) {
		this.name = name;
	}

	sayHi() {
		console.log(`Hi! My name is ${this.name}`);
	}
}

const me = new Person('Lee');
me.sayHi(); //Hi! My name is Lee
```

생성자 함수와 마찬가지로 클래스가 생성한 인스턴스는 프로토타입 체인의 일원이 된다. 생성자 함수의 역할을 클래스가 할 뿐이다. 결국 클래스는 생성자 함수와 같이 인스턴스를 생성하는 생성자 함수라고 볼 수 있다.

## 정적 메서드

정적(static) 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드를 말한다. 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드가 된다.

## 클래스에서 정의한 메서드의 특징

1. function 키워드를 생략한 메서드 축약 표현을 사용한다.
2. 객체 리터럴과는 다르게 클래스에 메서드를 정의할 때는 콤마가 필요 없다.
3. 암묵적으로 strict mode로 실행된다.
4. for ... in 문이나 Object.keys 메서드 등으로 열거할 수 없다.
5. 내부 메서드 [[Construct]]를 갖지 않는 non-constructor다. 따라서 new 연산자와 함께 호출할 수 없다.

# 클래스의 인스턴스 생성 과정

### 1. 인스턴스 생성과 this 바인딩

new 연산자와 함께 클래스를 호출하면 constructor의 내부 코드가 실행되기 앞서 암묵적으로 빈 객체가 생성된다. 이 빈 객체가 바로 클래스가 생성한 인스턴스다. 이때 클래스가 생성한 인스턴스의 프로토타입으로 클래스의 prototype 프로퍼티가 가리키는 객체가 설정된다. 그리고 암묵적으로 생성된 빈 객체, 즉 인스턴스는 this에 바인딩된다. 따라서 constructor 내부의 this는 클래스가 생성한 인스턴스를 가리킨다.

### 2. 인스턴스 초기화

constructor의 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티 값을 초기화한다. 만약 constructor가 생략되어싿면 이 과정도 생략된다.

### 3. 인스턴스 반환

클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환된다.

# 프로퍼티

## 인스턴스 프로퍼티

인스턴스 프로퍼티는 constructor 내부에서 정의해야 한다. 인스턴스 프로퍼티는 언제나 public 하다.

```jsx
class Person {
	constructor(name) {
		this.name = name
	}
}

const me = new Person('Lee')
console.log(me.name) //Lee
```

## 접근자 프로퍼티

자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(getter, setter)로 구성된 프로퍼티다.

```jsx
class Person {
	constructor(firstName, lastName){
		this.firstName = firstName;
		this.lastName = lastName;
	}

	get fullName() {
		return `${this.firstName} ${this.lastName}`;
	}

	set fullName(name) {
		[this.firstName, this.lastName] = name.split(' ');
	}
}

const me = new Person('Ungmo', 'Lee');
console.log(me); //{firstName: 'Ungmo', lastName: 'Lee'}

me.fullName = 'Heegun Lee';
console.log(me); //{firstName: 'Heegun', lastName: 'Lee'}
console.log(me.fullName); //Heegun Lee
```

getter는 호출하는 것이 아니라 프로퍼티처럼 참조하는 형식으로 사용하며, 참조 시에 내부적으로 getter가 호출된다. setter도 호출하는 것이 아니라 프로퍼티처럼 값을 할당하는 형식으로 사용하며, 할당 시에 내부적으로 setter가 호출된다.

setter는 단 하나의 값만 할당받기 때문에 단 하나의 매개변수만 선언할 수 있다.

## private 필드

private 필드의 선두에는 #을 붙여준다. private 필드를 참조할 때도 #을 붙여주어야 한다. private 필드는 클래스 내부에서만 참조할 수 있다.

```jsx
class Person {
	#name = '';

	constructor(name){
		this.#name = name;
	}
}

const me = new Person('Lee');
console.log(me.#name) //SyntaxError
```

private 필드는 반드시 클래스 몸체에 정의해야 한다. private 필드를 직접 constructor에 정의하면 에러가 발생한다.

# 참조

[클래스와 기본 문법](https://ko.javascript.info/class)
