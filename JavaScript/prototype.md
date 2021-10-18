자바스크립트는 클래스 기반 객체지향 프로그래밍 언어보다 효율적이며 더 강력한 객체지향 프로그래밍 능력을 지니고 있는 프로토타입 기반의 객체지향 프로그래밍 언어이다. 우리가 흔히 사용하는 Array, Maps, Sets 등도 모두 프로토타입을 기반으로 만들어졌다.

자바스크립트는 프로토타입을 기반으로 상속을 구현하여, 불필요한 중복을 제거한다. 만약 프로토타입이 없었다면 생성자 함수에 메서드를 넣어 사용하게 되어 엄청난 중복이 일어난다. 하지만 프로토타입을 사용하면 메서드가 오직 한개만 존재하게 된다. 

```jsx
// 자바스크립트 프로토타입 기반의 상속
function Greeting(name) {
  this.name = name
  //아래 과정은 사용하지 말아야 한다(중복 발생)
  //this.hello = function(){console.log(`hello ${this.name}`)
}

Greeting.prototype.hello = function() {
  console.log(`hello ${this.name}`)
}

const world = new Greeting('world')
world.hello() // output: hello world
```

## 프로토타입

![image](https://user-images.githubusercontent.com/67692759/137688350-95c96cd7-232c-4c60-9b6a-59d7d73d7b8d.png)


ECMA-262에서 prototype은 **‘object that provides shared properties for other objects’**로, 다른 객체에 공유 프로퍼티(메서드 포함)를 제공하는 객체이다.

알듯 말듯 모르겠는 내용이다. 생성자 함수를 더 알아보자.

### 자바스크립트가 객체를 생성하는 방법 (생성자 함수)

```jsx
const myObject = new Object({
	name: "object1"
})

console.log(typeof Object); // function
```

생성자(Constructor)를 사용하여 객체를 생성하는 것을 많이 보았을 것이다. 자바스크립트에서는 놀랍게도 이때 사용하는 Object의 type을 확인해보면 **함수**다! 여기서 우리는 Object또한 생성자 함수로 만들어졌음을 확인할 수 있다.

생성자 함수란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다. 아래 코드처럼 'new' 연산자와 생성자 함수를 사용하면 유사한 객체 여러 개를 쉽게 만들 수 있다.

```jsx
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("보라");

console.log(user.name); // 보라
console.log(user.isAdmin); // false
```

### 프로토타입?

이번에는 생성자 함수로 만든 객체의 타입을 확인해보자.

```jsx
const Person = function(firstName, birthYear){
    this.firstName = firstName;
    this.birthYear = birthYear;
}

const jonas = new Person('Jonas', 1991);

Person.prototype.calcAge = function(){
    console.log(2037-this.birthYear);
}

console.log(Person.prototype);
console.log(jonas.__proto__);
console.log(jonas.__proto__ === Person.prototype); //true
console.log(Person.prototype.isPrototypeOf(jonas)); //true
console.log(Person.prototype.isPrototypeOf(Person)); //false

Person.prototype.species = 'Homo Sapiens'; // 공통 property

console.log(jonas.species); //not owned property
console.log(jonas.hasOwnProperty('firstName')); //true
console.log(jonas.hasOwnProperty('species')); //false
```

new 연산자를 사용할 때 어떤 일이 일어나는 것일까?

> 1\. 새로운 {}가 만들어진다(비어있는 object가 생성된다)  
> 2\. 생성자 함수의 this가 새로운 object를 부른다(this={})  
> 3\. {}가 prototype으로 연결된다.  
> 4\. 함수가 {}를 return 한다.

이 과정을 사용하여 생성자 함수를 정의할 때 this값을 사용하는 것이다. new를 통해 새로 생성된 빈 오브젝트에 값을 정의하고, 이를 return받아 새로운 객체가 생성되는 것이다. 

위의 예시는 프로토타입을 이해하기 가장 좋은 예시이다. 메서드뿐만 아니라 속성 값도 프로퍼티로 설정할 수 있다. 하지만 이 값은 객체의 속성이 아님을 유의해야 한다.

#### constructor

```jsx
// 생성자 함수
function Person(name) {
	this.name = name;
}

const me = new Person('Lee');

// me 객체의 생성자 함수는 Person이다.
console.log(me.constructor == Person); //true
```

모든 객체는 constructor 프로퍼티를 갖는다. 이 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다. 이 연결은 생성자 함수가 생성될 때, 즉 함수 객체가 생성될 때 이뤄진다.

![image](https://user-images.githubusercontent.com/67692759/137688434-ad2444a7-1a72-49fe-b290-6a47abd40f2c.png)


말 그대로 생성자를 알 수 있게 해주는 프로퍼티다. 원본 객체의 constuctor 프로퍼티에 생성자 함수가 연결되어있기 때문에 새롭게 만들어진 객체는 자신의 원본 객체에 접근해서 이 프로퍼티를 참조함으로써 자신이 만들어질때 어떤 생성자 함수가 호출되었는지를 알 수 있다.

#### \_\_proto\_\_

\[\[Prototype\]\] 내부 슬롯에 직접 접근할 수 없기 때문에 \_\_proto\_\_ 접근자 프로퍼티를 통해 간접적으로 \[\[Prototype\]\] 네부 슬롯의 값 즉, 프로토타입에 접근할 수 있다.

![image](https://user-images.githubusercontent.com/67692759/137688463-a9bf4e3e-43a7-4817-b237-c4c7f67974a4.png)


Object.prototype을 제외한 자바스크립트 내의 모든 객체는 원본 객체를 기반으로 복사되어 생성되었기 때문에, 자신의 원본 객체로 연결되어있는 프로토타입 링크 또한 모든 객체가 가지고 있다. 이때 이 링크가 담기는 프로퍼티가 \_\_proto\_\_프로퍼티이다.

### 프로토타입 체인

자바스크립트는 객체의 프로퍼티(메서드 포함)에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 \[\[Prototype\]\] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. 이를 프로토타입 체인이라 한다. 프로토타입 체인은 자바스크립트가 객체지향을 프로그래밍의 상속을 구현하는 메커니즘이다.

자바스크립트 내의 사용되는 모든 객체들은 전부 프로토타입 기반 방식으로 정의되고 생성된다. 즉, String, Boolean,Array와 같이 우리가 일반적으로 사용하고 있는 빌트인 객체들도 모두 같은 방식을 사용해서 만들었다는 것이다.

자바스크립트의 모든 것들은 Object로부터 만들어 졌기 때문에 함수의 프로토타입인 Object.prototype을 시작으로 해서 복제된다.

![image](https://user-images.githubusercontent.com/67692759/137688498-0377180a-ffa9-4115-9f76-944f839deaba.png)
