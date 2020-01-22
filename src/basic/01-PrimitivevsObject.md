## Primitive(값) vs Object(참조)

## Primitive Type

- String : 텍스트를 셋팅하는데 사용하는 타입.
- Number : 숫자를 셋팅하는데 사용하는 타입. 기본적으로 소수점도 가능하다.(infinity, -inifinity, NaN 표현이 가능하다.)
- Null : null타입은 정확히는 1개의 값은 가지고 있지만 비어있다는 뜻이다.
- Undefined : 값이 할당되지 않는 것을 나타내는 타입.
- Boolean : true 또는 false 로 나타내는 타입.
- Symbol : 새로 추가된 타입으로 **unique하고 immutable한 원시값** 으로 사용된다.(ES6)

### Primitive Type의 생성 방법

1. Literal
- Literal로 생성한다고 하면 우리가 가장 많이 사용하는 방법

```js
var bol = true;
var str = "hello";
var num = 3.14;
var nullType = null;
var undef = undefined;

var bol2;
var str2;
bo2 = false
str2 = "world"
```

2. Wrapper Object

- Wrapper Object를 사용해서 만든다고 하면 Constructor를 사용해서 만드는 것
- 즉, `new` 를 사용하여 생성

```js
new Boolean(false);
new String("world");
new Number(42);

Symbol("foo"); //Symbol 타입의 생성방법
```

### Literal vs Wrapper

```js
typeof true; //"boolean"
typeof Boolean(true); //"boolean"
typeof new Boolean(true); //"object"
typeof (new Boolean(true)).valueOf(); //"boolean"
     
typeof "abc"; //"string"
typeof String("abc"); //"string"
typeof new String("abc"); //"object"
typeof (new String("abc")).valueOf(); //"string"
     
typeof 123; //"number"
typeof Number(123); //"number"
typeof new Number(123); //"object"
typeof (new Number(123)).valueOf(); //"number"
```

 Literal로 생성한 것의 타입은 6가지 중 하나로 나오게 된다. 그런데 new를 사용하여 Wrapper Object로 만들게 되면 Object타입이 나오게 된다. 사용을 하려면 valueOf라는 Function을 사용해야만 입력한 값이 나오게 된다.

### 값 타입

```js
var a = 13         // assign `13` to `a`
var b = a          // copy the value of `a` to `b`

b = 37             // assign `37` to `b`

console.log(a)     // => 13
```

b의 값을 변경을 했지만 a에는 영향이 가지 않았다. 이유는 2개의 값이 저장된 공간이 다르기 때문이다.

## Object Type

- Array : 우리가 알고 있는 배열, 리스트의 형태를 가지고 있다.
- Function : Javascript에서는 Function Object가 존재하지만 결국 Function도 Object.
- Object : Map처럼 사용하는 즉, key : value의 형태로 사용하고 있는 Object.

```js
var a = { c: 13 }  // assign the reference of a new object to `a`
var b = a          // copy the reference of the object inside `a` to new variable `b`
b.c = 37           // modify the contents of the object `b` refers to
console.log(a)     // => { c: 37 }
```

```js
var a = [];
var b = a;

a.push(1);

console.log(a); // [1]
console.log(b); // [1]
console.log(a === b); // true
```

```js
function changeAgeImpure(person) {
    person.age = 25;
    return person;
}
var alex = {
    name: 'Alex',
    age: 30
};
var changedAlex = changeAgeImpure(alex);

console.log(alex); // -> { name: 'Alex', age: 25 }
console.log(changedAlex); // -> { name: 'Alex', age: 25 }
```

원시타입과는 다르게 복사한 것을 변경을 했더니 기존 객체에도 영향이 간다. 이유는 **같은 값의 주소**를 복사했기 때문이다.

---

#### 🙏 Reference

- [ImD/Dev-Docs - javascript Type](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/B_Type.md)