## 모듈(Module)

자바스크립트(`ES5`)에서 기본적으로 모듈 기능이 없다.
기본적으로 자바스크립트에서 **변수는 전역(global)에 할당되기 때문에 모듈을 구현하기 위해서는 `Namespace Pattern` 혹은 [Module Pattern](https://bkdevlog.netlify.com/posts/oop-encapsulation-of-js)과 같은 기법이 필요**했다.

이러한 상황에서 클라이언트 사이드에서뿐만이 아니라 범용적인 사용이 일어나면서 모듈화의 필요성이 대두되었다. 이에 따라 [CommonJS와 AMD](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/AMD%EC%99%80%20CommonJS.md) 이렇게 2개의 진영으로 나뉘게 되었다.
우리가 잘 알고 있는 `Node.js`는 `CommonJS`의 모듈화 방식을 따르고 있다.

`ES6`에서는 **클라이언트 사이드에서도 모듈화를 제공하기 위해 `export`와 `import`가 추가**되었다.
단, `ES6`의 모듈 기능은 대부분의 브라우저에서는 지원하지 않기 때문에 `RequireJS`와 같은 모듈 로더나 `Webpack`과 같은 모듈 번들러와 함께 `babel`과 같은 트랜스파일러를 사용하여야 한다.

## export

ES6의 모듈은 보통 **파일 단위**로 구성되며 독립적인 파일 스코프를 가지기 때문에 **외부에서 모듈의 기능을 사용하고 싶다면 위와 같이 `export`를 해줘야한다.**

```js
//module.js
export const message = "this is variable";

export function sayHello() {
  console.log("Hello World");
}

export function sayName(name) {
  console.log(`Hi ${name}`);
}

export class Person {
  constructor(name, job) {
    this.name = name;
    this.job = job;
  }
}
```

위와 같이 각각의 변수, 함수, 클래스에 `export`키워드를 붙여 export할 수 있고 아래와 같이 **하나의 객체로 묶어 한 번에 export할 수도 있다.**

```js
//module.js
const message = "this is variable";

function sayHello() {
  console.log("Hello World");
}

function sayName(name) {
  console.log(`Hi ${name}`);
}

class Person {
  constructor(name, job) {
    this.name = name;
    this.job = job;
  }
}

export { message, sayHello, sayName, Person };
```

## import

ES6에서 export한 모듈을 사용하기 위해서는 해당 파일에서 `import`키워드를 사용하여 가져와 쓰면 된다.

```js
import { message, sayHello, sayName, Person } from "./module";

console.log(message); //this is variable
console.log(sayHello()); //Hello World
console.log(sayName("BKJang")); //Hi BKJang
console.log(new Person("BKJang", "Developer")); //Person { name : BKJang, job: Developer }
```

위와 같이 각각를 import하지 않고 **한꺼번에 import하거나 이름을 변경하여 import 할 수도 있다.**

```js
//한꺼번에 묶어서 import
import * as module from "./module";

console.log(module.sayName("BKJang")); //Hi BKJang
```

```js
//이름을 변경하여 import
import { sayHello as hello } from "./module";

console.log(hello()); //Hello World
```

## default

모듈에서 하나만 export할 경우에는 `default`키워드를 사용하면 된다.

```js
//Person.js
export default class Person {
  constructor(name) {
    this.name = name;
  }
}
```

```js
//Person.js
class Person {
    //...
}

export default
```

이를 import할 때는 **`{}`없이 해당 모듈을 임의의 이름으로 가져와 사용**하면 된다.

```js
import Person from "./Person";
```

---

#### 🙏 Reference

- [모듈](https://poiemaweb.com/es6-module)
- [import(MDN web docs)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import)
- [export(MDN web docs)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export)
