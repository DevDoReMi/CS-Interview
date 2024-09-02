# this의 용법 (중요도 4)

## Table of Conetents

1. [this란?](#this란)
2. [요약](#요약)
3. [함수 호출 방식](#함수-호출-방식)

## this란?

this는 함수를 호출할 때 생성되는 실행 컨텍스트 객체이다.
현재 실행중인 함수 내에서 this키워드가 사용된 위치에 따라 참조하는 객체가 동적으로 결정된다.
함수가 호출될 때 '참조 객체가 결정'되기 때문에, **함수 호출 방법에 따라 this가 참조하는 객체가 달라지게 된다**.

## 요약

- 함수가 객체의 메서드로 호출될 때, this는 해당 객체를 참조한다.
- 함수가 일반적인 함수로 호출될 때, this는 전역 객체(window 또는 global)를 참조힌다.
- 함수가 생성자로 호출될 때, this는 새로 생성된 객체를 참조한다.
- call(), apply(), bind() 메서드를 사용하여 명시적으로 this의 값을 지정할 수 있다.

## 함수 호출 방식

1. 함수 호출
2. 메소드 호출
3. 생성자 함수 호출
4. apply, call, bind 호출

```
var foo = function () {
  console.dir(this);
};

// 1. 함수 호출
foo(); // window
// window.foo();

// 2. 메소드 호출
var obj = { foo: foo };
obj.foo(); // obj

// 3. 생성자 함수 호출
var instance = new foo(); // instance

// 4. apply/call/bind 호출
var bar = { name: 'bar' };
foo.apply(bar);  // bar
foo.call(bar);   // bar
foo.bind(bar)(); // bar
```

### 1. 함수 호출

기본적으로 this 객체는 전역객체에 바인딩된다.

- 전역함수, 내부함수, 메소드의 내부함수, 콜백함수의 경우도 전역객체에 바인딩 됨

전역객체는 모든 객체의 유일한 최상위 객체를 의미한다.

- brower-side에서는 window
- server-side에서는 global

전역객체는 전역 스코프를 갖는 전역변수를 프로퍼티로 소유한다.
글로벌 영역에 선언한 함수는 전역객체의 프로퍼티로 접근할 수 있는 전역변수의 메소드이다.

```
console.log(this === window); // true

function myFunction() {
  console.log(this === window); // true
}

myFunction();

```

### 2. 메소드 호출

함수가 객체의 프로퍼티 값이면 메소드로서 호출된다.

이때 메소드 내부의 this는 해당 메소드를 소유한 객체, 즉 해당 메소드를 호출한 객체에 바인딩된다.

프로토타입 객체도 메소드를 가질 수 있다. 프로토타입 객체 메소드 내부에서 사용된 this도 일반 메소드 방식과 마찬가지로 해당 메소드를 호출한 객체에 바인딩된다.

```
const myObject = {
  name: 'sujeong',
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

myObject.greet(); // "Hello, my name is sebnson"
```

### 3. 생성자 함수 호출

자바스크립트의 생성자 함수는 말 그대로 객체를 생성하는 역할을 한다.
하지만 자바와 같은 객체지향 언어의 생성자 함수와는 다르게 그 형식이 정해져 있는 것이 아니라 **기존 함수에 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작**한다.

즉, 생성자 함수가 아닌 **일반 함수에 new 연산자를 붙여 호출하면 생성자 함수처럼 동작할 수 있다**. 따라서 일반적으로 생성자 함수명은 첫문자를 대문자로 기술하여 혼란을 방지하려는 노력을 한다.

new 연산자와 함께 생성자 함수를 호출하면 this 바인딩이 메소드나 함수 호출 때와는 다르게 동작한다.

```
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const sujeong = new Person('sebnson', 26);
console.log(sujeong.name); // "sebnson"
console.log(sujeong.age); // 26
```

### 4. apply, call, bind 호출

this를 명시적으로 바인딩할 수 있는 방법.
apply, call, bind 메소드들은 모든 함수 객체의 프로토타입 객체인 Function.prototype 객체의 메소드이다.

- apply()
  - 주어진 this의 값과 배열(or 유사 배열 객체)로 제공되는 **arguments**로 함수 호출
- call()
  - 주어진 this값 및 각각 전달된 인수와 함께 함수 호출
- bind()
  - bind 호출 시 새로운 함수 생성.
  - 받게 되는 첫 인자의 value로 this 키워드를 설정하고, 이어지는 인자들은 바인드된 함수의 인수에 제공한다.

apply, call, bind에서 첫 번째 인자로 다른 것을 넣어주는 것이 this를 바구는 방법 중 하나이다.

```
func.apply(thisArg, [argsArray])
func.call(thisArg[, arg1[, arg2[, ...]]])
func.bind(thisArg[, arg1[, arg2[, ...]]])
```

```
// call 예시
function myFunction() {
  console.log(`Hello, my name is ${this.name}`);
}

const myObject = { name: 'sebnson' };

myFunction.call(myObject); // "Hello, my name is sebnson"
```

```
// bind 예시
const myObject = { name: 'sebnson' };

function myFunction() {
  console.log(`Hello, my name is ${this.name}`);
}

const myBoundFunction = myFunction.bind(myObject);
myBoundFunction(); // "Hello, my name is sebnson"
```

### 5. 그 외의 경우

- strict mode: undefined로 초기화된다.

### ref.

https://github.com/Esoolgnah/Frontend-Interview-Questions/blob/main/Notes/important-4/this.md
https://suzzeong.tistory.com/127
https://yooneeee.tistory.com/123
