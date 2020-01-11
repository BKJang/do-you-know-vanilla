## 화살표 함수(Arrow Function)

**화살표 함수는 `function` 대신 `=>`를 사용**함으로써 좀 더 간결하게 함수를 선언할 수 있다.

또한 화살표 함수는 익명 함수로만 사용할 수 있기 때문에 **함수 표현식**을 사용한다.

```js
const foo = () => {...} //매개변수가 없을 때
const foo = x => {...} //매개변수가 하나일 때
const foo = (x, y) => {...} //매개변수가 여러 개일 때

const foo = x => { return x; }
const foo = x => x; // 함수의 블록이 한줄이라면 중괄호와 return을 생략

const sum = (x, y) => {
    return x + y;
}

console.log(sum(1, 2)); //3
```

```js
//ES5
var arr = ["JS", "Java", "Go"];
var foo = arr.map(function(element) {
  return { Lang: element };
});

console.log(foo); //[{Lang: "JS"}, {Lang: "Java"}, {Lang: "Go"}]

//ES6
const arr = ["JS", "Java", "Go"];
const foo = arr.map(element => {
  return { Lang: element };
});

console.log(foo); //[{Lang: "JS"}, {Lang: "Java"}, {Lang: "Go"}]
```

### 화살표 함수에서의 this 바인딩

ES5에서는 **함수의 호출 방식에 따라 this가 동적으로 바인딩**이 이뤄진다.

[ES5의 this 바인](https://github.com/BKJang/do-you-know-vanilla/issues/7)

하지만 화살표 함수에서는 this가 무조건 상위 스코프의 this를 가리킨다.

즉 정적인 방식으로 this가 바인딩이 되는데 이를 **Lexical this** 라고 한다.

위의 소스를 화살표 함수를 이용해서 바꾸면 `var that = this;`라는 구문을 쓸 필요가 없다.

```js
const lang = "Korean";

const obj = {
  lang: "English",
  outerFunc() {
    //ES6의 축약 메서드 표현
    console.log("outerFunc : ", this.lang);

    innerFunc1 = () => {
      console.log("innerFunc1 : ", this.lang);

      innerFunc2 = () => {
        console.log("innerFunc2 : ", this.lang);
      };

      innerFunc2();
    };

    innerFunc1();
  }
};

obj.outerFunc();

/*
outerFunc : English
innerFunc1 : English
innerFunc2 : Engilsh
*/
```

### 항상 화살표 함수일까?

화살표 함수는 위에서 본 것 처럼 정적으로 this를 바인딩(Lexical this)를 지원하기 때문에 콜백 함수로 쓰기 매우 편하다. 하지만, 주의해서 써야할 경우가 몇 가지 있다.

### addEventListener의 콜백 함수 선언

```js
const btn = document.getElementById("submitBtn");

btn.addEventListener("click", () => {
  console.log(this); //Window
});
```

위에서 볼 수 있듯이 `addEventListener`의 **콜백 함수를 화살표 함수로 선언하면 `this`는 `window`에 바인딩되므로 그냥 일반함수를 사용하여 선언**하여야 한다.

### 객체의 메서드에 선언

객체의 메서드를 선언할 때, **화살표 함수를 쓰면 그 객체에 this가 바인딩되지 않고 전역(window)에 바인딩**된다.

```js
var lang = "Korean";

const obj = {
  lang: "English",
  foo: () => {
    console.log("outerFunc : ", this.lang);
  }
};

obj.foo(); //outerFunc : Korean
```

위에선 English가 나온다고 생각할 수도 있다. <br/>하지만, `foo` 선언할 때 화살표 함수를 사용했고 이에 따라 **상위 컨텍스트인 `window`에 `this`가 바인딩** 되기 때문에 결과는 Korean이 나온다.

따라서 원하는 결과가 English라면 축약 메서드 표현법으로 정의하는 것이 맞다.

```js
var lang = "Korean";

const obj = {
  lang: "English",
  foo() {
    console.log("outerFunc : ", this.lang);
  }
};

obj.foo(); //outerFunc : English
```

### 프로토타입 객체의 메서드 선언

프로토타입 객체에 메서드를 화살표 함수로 정의하면 객체의 메서드에 화살표 함수로 선언할 때와 같이 **`this`가 `window`에 바인딩**된다.

```js
const devleoper = {
  name: "BKJang"
};

Object.prototype.renderData = () => console.log(this.name);

devleoper.renderData(); //undefined
```

### 생성자 함수 선언

결론부터 말하면, **화살표 함수는 `prototype` 프로퍼티를 갖고 있지 않다.** 따라서 생성자 함수를 선언할 때 화살표 함수를 쓰면 인스턴스를 생성할 수 없다.

```js
const Person = name => {
  this.name = name;
};

const jang = new Person("BKJang"); //Uncaught TypeError: Person is not a constructor
```
