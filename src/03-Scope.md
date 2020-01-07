## Functional Scope vs Block Scope

## Functional Scope

자바스크립트는 **함수를 단위로 Scope를 구분한다.** 즉 같은 함수 안에서 선언된 변수들은 같은 레벨의 Scope를 가지게 되는 것이다. 각각의 함수는 독립적인 Scope를 가지게 되어 다른 함수의 Scope에 접근을 할 수 없다.

```javascript
// Global Scope
function someFunction() {
  if (true) {
    var name = "BKJang";
  }
  console.log(name); //BKJang
}
```

위와 같이 Global Scope에 `someFunction()` 을 선언하고 내부에 if문 괄호 안에 선언한 변수는 **someFunction function Scope** 에 붙게 된다. 함수를 단위로 스코프가 생기기 때문에 `name`을 출력하면 `undefined`가 아닌 `BKJang`이 출력된다.

## Block Scope

Block Statement는 우리가 많이 보는 if문, switch문, for, while문이다. 이러한 문장들은 괄호로 감싸진 부분이 존재하지만 새로운 Scope를 만들지는 않는다. Block Statement 안에서 정의한 변수는 가장 가까운 함수의 Scope에 붙게 된다.

```javascript
if (true) {
  // this 'if' conditional block doesn't create a new scope
  var name = "BKJang"; // name is still in the global scope
}

console.log(name); // logs 'sseon'
```

`ES6`에서는 `let`, `const`가 추가 되었다. 이 2개는 `var` 대용으로 사용된다. 그러나 그보다 더 중요한 개념이 들어간다. 바로 **Block Level Scope** 라는 것이다. 기존의 자바스크립트는 위에서 본 것처럼 **Functional Scope** 이다. 그러나 `let`, `const` 를 사용하게 되면 **Block Level Scope** 지원이 가능하다.

```javascript
if (true) {
  // this 'if' conditional block doesn't create a new scope
  var name = "BKJang"; // name is still in the global scope
  let likes = "Coding";
  const lang = "Javascript";
}

console.log(name); // 'BKJang'
console.log(likes); // Uncaught ReferenceError: likes is not defined
console.log(lang); // Uncaught ReferenceError: lang is not defined
```

`var`와는 다르게 `let`, `const`는 Block Statement내에서 **Local Scope** 를 지원한다. 즉 이제 Scope가 가장 가까운 function에 붙는 것이 아닌 해당 Block에 붙게 되는 것이다.

**참고로 Global Scope는 응용 프로그램이 살아있을 때까지 유효하며, Local Scope은 함수가 호출되고 실행되는한 유지가 된다.**
