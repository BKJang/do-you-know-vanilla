## 실행 컨텍스트

실행 컨텍스트는 자바스크립트가 동작하는 원리라고 할 수 있다.

쉽게 말하면, **코드가 실행되는 환경**이라고 보면 된다.

- 전역 컨텍스트 생성 후, **함수 호출 시마다 함수 컨텍스트가 생긴다.**

- 컨텍스트 생성 시 컨텍스트 안에 `변수객체(arguments, variable)`, `scope chain`, `this`가 생성된다.

- 컨텍스트 생성 후 함수가 실행되는데, **사용되는 변수들은 변수 객체 안에서 값을 찾고, 없다면 스코프 체인을 따라 올라가며 찾는다.**

- **함수 실행이 끝나면 해당 컨텍스트는 사라지고, 페이지가 종료되면 전역 컨텍스트는 사라진다.**

### 실행 컨텍스트 스택

코드가 실행 될 때, **실행 컨텍스트 스택(Stack)** 이 생성하고 소멸한다.

현재 **실행 중인 컨텍스트에서 관련없는 코드(예를 들어, 다른 함수)가 실행되면 새로운 컨텍스트가 생성**된다.

```js
var global = "global";

function foo() {
  var local1 = "local1";

  function bar() {
    var local2 = "local2";
    console.log(local1, local2, global); //local1 local2 global
  }

  bar();
}

foo();
```

![JavaScript](https://bkdevlog.netlify.com/assets/img/js_ec_stack.png)

### 변수 객체(Variable Object)

실행 컨텍스트가 생성되면 자바스크립트 엔진은 **실행에 필요한 여러 정보들을 담을 객체를 생성**한다. 이를 **Variable Object(VO / 변수 객체)** 라고 한다.

변수 객체는 **arguments(인수 정보)** 와 **variable(스코프의 변수)** 을 담고 있고, 전역 컨텍스의 경우와 함수 컨텍스트의 경우에 가리키는 객체가 다르다.

#### 전역 컨텍스트

전역 컨텍스트의 경우, 변수 객체는 `arguments`를 가지지 않는다.

그리고 **변수 객체는 모든 전역 변수, 전역 함수 등을 포함하는 전역 객체(Global Object / GO)를 가리킨다.**

전역 객체는 전역 변수와 전역 함수를 프로퍼티로 가진다.

![JavaScript](https://bkdevlog.netlify.com/assets/img/js_global_context.png)

#### 함수 컨텍스트

함수 컨텍스트의 경우, **변수 객체는 Activation Object(AO / 활성 객체)를 가리킨다.**

또한, 전역 컨텍스트와 다르게 매개변수와 인수들의 정보를 배열의 형태로 담고 있는 유사 배열 객체 `arguments`도 가진다.

![JavaScript](https://bkdevlog.netlify.com/assets/img/js_function_context.png)

### 스코프 체인(Scope Chain)

스코프 체인은 **현재 컨텍스트의 유효 범위를 나타내는 스코프 정보를 담고 있으며**, 연결 리스트의 형태와 유사하게 생성된다.

이 리스트를 이용해 현재 컨텍스트의 변수와 상위 실행 컨텍스트의 변수에도 접근할 수 있다.

이 리스트는 **현재 실행 컨텍스트의 활성 객체**를 먼저 가리키고 순차적으로 **상위 컨텍스트의 활성 객체**를 가리키고 마지막으로 **전역 객체**를 가리킨다.

![JavaScript](https://bkdevlog.netlify.com/assets/img/js_scope_chain.png)

> 즉, 스코프 체인은 식별자 중 **변수를 검색하는 것**을 말하고, 변수가 아닌 **객체의 프로퍼티를 검색하는 것**을 프로토타입 체인이라고 한다.

---

#### :pray: Reference

- 인사이드 자바스크립트 (송형주, 고형준)
- [Poiemaweb - 실행 컨텍스트와 자바스크립트의 동작 원리](https://poiemaweb.com/js-execution-context)
