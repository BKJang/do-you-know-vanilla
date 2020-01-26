## 네임스페이스 패턴(Namespace Pattern)과 IIFE

전역 변수를 많이 쓰면 안좋다고 흔히들 말한다.
그 이유를 알 수 있는 간단한 예를 보자.

```javascript
var x = 100;

function test() {
    x = 10;
    console.log('10이 나오겠지?', x);
}

test();
console.log('100을 출력해볼까 ?', x);

/*
10이 나오겠지? 10
100을 출력해볼까 ? 10
*/
```

**지역 스코프에서 전역변수를 참조할 수 있으므로** 전역변수의 값도 변경할 수 있다.
**내부 함수의 경우에는, 전역변수는 물론 상위 함수에서 선언한 변수에 접근/변경이 가능**하다.

프로젝트가 클수록, 협업이 이루어질수록 전역 변수가 많아지면 원하는 결과가 아닌 다른 결과가 나타날 수 있다.


### 네임스페이스 패턴(Namespace Pattern)

네임스페이스 패턴은 **말 그대로 이름 공간을 선언하여 다른 공간과 구분하는 패턴**이라고 보면 된다.

```javascript
var APP_GLOBAL = {
    name : 'BKJang',
    age : '25',
    getInfo : function() {
        console.log('name :', this.name, 'age :', this.age);
    }
}

console.log(APP_GLOBAL); //{name: "BKJang", age: "25", getInfo: ƒ}
console.log(APP_GLOBAL.name, APP_GLOBAL.age); //BKJang 25
APP_GLOBAL.getInfo(); //name : BKJang age : 25
```

이처럼 **전역 변수 사용을 위해 전역 객체 하나를 만들어 사용**하는 것이다.

### 즉시 실행 함수 표현식(IIFE, Immediately-Invoked Function Expression)

즉시 실행 함수를 사용하면 **함수가 실행되고 전역에서 사라진다.** 이 방법으로 라이브러리를 많이 만들곤 한다.

```javascript
(function moduleFunction() {

  var a = 3;
  
  function helloWorld(){
    console.log('Hello');
  }

  helloWorld(); //Hello
})();

helloWorld(); //Uncaught ReferenceError: helloWorld is not defined
```

즉시실행함수가 실행되고 전역에서 사라지기 때문에 그 밖에선 출력 값이 에러가 발생하는 것을 볼 수 있다. 

```javascript
var singleton = (function () {

  var a = 3;
  
  function helloWorld(){
    console.log('Hello');
  }

  return {
    a : a,
    sayHello: helloWorld
  }
})();

singleton.sayHello(); //Hello
console.log(singleton.a); //3

```

위와 같이 **반환 값을 변수에 담아 전역 변수를 한 번 만 사용**하여 전역 변수의 사용을 줄일 수도 있다.

---

#### 🙏 Reference

- [JavaScript: 네임스페이스 패턴(Namespace Pattern) 바로 알기](http://www.nextree.co.kr/p7650/)