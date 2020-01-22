## Spread연산자 & rest파라미터

### rest 파라미터

rest 파라미터는 Spread 연산자(`...`)를 사용하여 파라미터를 정의한다.
기존에 ES5에서는 가변 파라미터를 정의할 때 `arguments`객체를 사용할 수 있었지만 이를 `rest 파라미터`로 대체할 수 있다.

```js
//ES5
function foo() {
  console.log(Array.isArray(arguments));
  console.log(arguments);
}

foo(1, 2, 3, 4, 5);
/*
false
{'0': 1, '1': 2, '2': 3, '3': 4, '4': 5, length: 5}
*/
```

```js
//ES6
function foo(...rest) {
  console.log(Array.isArray(rest));
  console.log(rest);
}

foo(1, 2, 3, 4, 5);
/*
true
[1, 2, 3, 4, 5]
*/
```

위의 결과를 보면 arguments 객체와 rest 파라미터의 중요한 차이를 알 수 있다.

**`arguments`객체는 유사배열 객체**다. 따라서 `Array.isArray(arguments)`의 결과는 false를 반환한다.

여기서 큰 차이가 발생하는데 **유사배열객체는 배열의 메서드를 사용할 수 없다.** 배열의 메서드를 사용하기 위해서는 이를 **배열로 변환하는 과정을 거쳐야하는 불편함**이 있다. <br/>
하지만 가변 인자 함수를 rest 파라미터로 정의하면 파라미터는 배열의 형태로 넘어온다.

또한 ES6의 [화살표 함수(Arrow Function)](https://bkjang.github.io/arrow_function/)에서는 `arguments`를 사용할 수 없다.

```js
//ES6 화살표 함수
const foo = () => {
  console.log(arguments);
};

foo(1, 2, 3, 4, 5); //Uncaught ReferenceError: arguments is not defined
```

> - `rest` 파라미터는 `arguments`와 달리 **배열**로 파라미터가 넘어온다.
> - ES6의 **화살표 함수에서는 `arguments`를 사용할 수 없다.**

### Spread 연산자

Spread 연산자는 말그대로 전개 연산자다. **배열 또는 Iterable object(반복 가능한 객체)의 엘리먼트를 하나씩 분리하여 전개**한다.

```js
let a = "Hello";
let arr = [...a];

console.log(arr); //["H", "e", "l", "l", "o"]
```

### Spread 연산자의 활용

- **concat**

ES5에서는 배열을 합칠 때 `concat`을 사용했었다. 이를 `Spread`연산자로 대체할 수 있다.

```js
//concat
var arr1 = [5, 6];
var arr2 = [1, 2, 3, 4];

console.log(arr2.concat(arr1)); //[1, 2, 3, 4, 5, 6]
console.log(arr1.concat(arr2)); //[5, 6, 1, 2, 3, 4]
```

```js
//ES6 Spread Operator
let arr1 = [5, 6];
let arr2 = [1, 2, 3, 4, ...arr1];

console.log(arr2); //[1, 2, 3, 4, 5, 6]
console.log([1, 2, ...arr1, 3, 4]); //[1, 2, 5, 6, 3, 4]
```

단순히 앞, 뒤에 배열의 요소를 붙이는데는 `concat`이 성능이 더 좋다. 하지만 중간에 특정 배열의 값을 추가하고 싶다면 `Spread`연산자를 사용하는 것도 좋은 방법이다.

- **split**

문자열을 배열로 변환할 때 많이 쓰이는 함수가 `split()`이다. 이 또한 Spread 연산자를 활용하면 좀 더 편하게 변환할 수 있다.

```js
//split

var a = "Hello";
var arr = a.split("");

console.log(arr); //["H", "e", "l", "l", "o"]
```

```js
//ES6 Spread Operator

let a = "Hello";
let arr = [...a];

console.log(arr); //["H", "e", "l", "l", "o"]
```

- **함수의 인자로 사용**

기존에 ES5에서는 배열의 각 요소를 개별적인 파라미터로 전달하고 싶은 경우, `Function.prototype.apply`를 사용하는 것이 일반적이었다. <br/>하지만 ES6의 `Spread` 연산자를 활용하여 함수의 인자에 들어가는 배열을 개별요소로 전달할 수 있다.

```js
//ES5 apply
var arr = [1, 2, 3];

function sum(a, b, c) {
  console.log(a, b, c); //1 2 3
  return a + b + c;
}

console.log(sum.apply(null, arr)); //6
```

```js
//ES6 Spread Operator
let arr = [1, 2, 3];

const sum = (a, b, c) => a + b + c;

console.log(sum(...arr)); //6
```

- **객체에서 사용**

객체는 Iterable Object아니지만 Spread 연산자를 사용하면 객체를 손쉽게 병합 또는 변경할 수 있다.

```js
let obj1 = {
  name: "BKJang",
  job: "Developer"
};

let obj2 = {
  ...obj1,
  lang: "Korean"
};

console.log(obj2); //{name: "BKJang", job: "Developer", lang: "Korean"}
```

Spread 연산자를 활용하면 유사배열객체(arguments, HTMLCollection 등)를 배열로 변환하기도 편하다.

```js
function foo() {
  let args = arguments;
  let arr = [...args];

  console.log(Array.isArray(args)); //false
  console.log(Array.isArray(arr)); //true
  console.log(arr); //
}

foo(1, 2, 3, 4, 5); //[1, 2, 3, 4, 5]
```

---

#### 🙏 Reference

- [MDN Web Docs - Spread 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [[ES6] 4. Spread, Rest parameter
  ](https://jaeyeophan.github.io/2017/04/18/ES6-4-Spread-Rest-parameter/)
- [파라미터 기본값, Rest 파라미터, Spread 연산자](https://poiemaweb.com/es6-extended-parameter-handling)
