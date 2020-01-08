## JavaScript의 this

자바스크립트에서 `this`의 바인딩은 함수의 호출 방식에 따라 결정된다.

- **객체의 메서드 호출**
- **일반 함수 호출**
- **생성자 함수의 호출**
- **`call`과 `apply`를 이용한 `this` 바인딩**
- **ES6의 화살표 함수**

### 객체의 메서드 호출

```js
var obj = {
  organization: "Im-D",
  sayHello: function() {
    return "Welcome to " + this.organization;
  }
};

console.log(obj.sayHello());
```

객체의 메서드를 호출할 때 `this`는 **해당 객체에 바인딩**된다.

### 일반 함수 호출

```js
var organization = "Im-D";

function sayHello() {
  var organization = "Kyonggi";
  return "Welcome to " + this.organization;
}

console.log(sayHello());
```

일반 함수를 호출할 때, 자바스크립트의 `this`는 **전역 객체(window 객체)에 바인딩** 된다.

### 생성자 함수의 호출

```js
function Organization(name, country) {
  this.name = name;
  this.country = country;
}

var imD = new Organization("Im-D", "South Korea");
var kyonggi = Organization("Kyonggi", "South Korea");

console.log(imD);

console.log(kyonggi);
```

생성자 함수를 `new`키워드를 통해 호출할 경우, **새로 생성되는 빈 객체에 바인딩** 된다. 단, `new`키워드를 사용하지 않으면 `this`는 전역객체에 바인딩된다.

### `call`, `apply`, `bind`를 활용한 `this`바인딩

#### call

```js
function Module(name) {
  this.name = name;
}

Module.prototype.getName = function() {
  const changeName = function() {
    console.log(this);
    return this.name + "입니다.";
  };
  // return changeName.call(this, 1,2,3,4);
  return changeName.call(this);
};

const module = new Module("BKJang");

console.log(module.getName());
```

#### apply

```js
function Module(name) {
  this.name = name;
}

Module.prototype.getName = function() {
  const changeName = function() {
    console.log(this);
    return this.name + "입니다.";
  };

  // return changeName.apply(this, [1,2,3,4]);
  return changeName.apply(this);
};

const module = new Module("BKJang");

console.log(module.getName());
```

또한 `call`이나 `apply`메서드를 활용하여 **유사배열 객체를 일반 배열로 바꿀 수도 있다.**

```js
function sayHello() {
  console.log(arguments);
  var args = Array.prototype.slice.apply(arguments);
  console.log(args);
}

sayHello("Im-D", "South Korea");
```

`call`과 `apply`는 내부 함수에서 사용할 this를 설정하고 함수 바로 실행까지 해주지만, `bind`는 `this`만 설정해주고 함수 실행은 하지 않고 함수를 반환한다.

```js
function Module(name) {
  this.name = name;
}

Module.prototype.getName = function() {
  const changeName = function() {
    console.log(this);
    return this.name + "입니다.";
  };
  let bindChangeName = changeName.bind(this);
  return bindChangeName();
};

const module = new Module("BKJang");

console.log(module.getName());
```

### 화살표 함수

```js
var obj = {
  organization: "Im-D",
  outerFunc: function() {
    var that = this;
    console.log(this.organization);

    innerFunc = function() {
      console.log(that.organization);
      console.log(this.organization);
    };

    innerFunc();
  }
};

obj.outerFunc();
```

```js
var obj = {
  organization: "Im-D",
  outerFunc: function() {
    console.log(this.organization);

    innerFunc = () => {
      console.log(this.organization);
    };

    innerFunc();
  }
};

obj.outerFunc();
```

`ES5`에서는 원래 내부 함수에서의 `this`는 `window`객체에 바인딩 되었기 때문에 `var that=this;`와 같이 선언하여 `that`에 `this`를 할당하고 내부 함수에서는 `that`을 활용하는 방식을 사용했었다.

하지만, `ES6`에서 등장한 **화살표 함수에서는 this가 무조건 상위 스코프의 this를 가리킨다.**
이에 따라 내부함수에서 `var that=this;`와 같은 구문을 사용할 필요가 없다.
이처럼 정적으로 `this`가 바인딩되기 때문에 **Lexical this**라고 한다.

---

#### :pray: Reference

- [SeonHyungJo - Javascript-Book](https://seonhyungjo.github.io/Javascript-Book/Basic/11-Call-Apply-Bind.html)
- [Im-D/Dev-Docs -Javascript의 this](https://github.com/Im-D/Dev-Docs/edit/master/Javascript/JavaScript%EC%9D%98%20this.md)
- [Zerocho - 자바스크립트의 this는 무엇인가](https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb)
