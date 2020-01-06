## 명시적 변환 vs 암묵적 변환

`Number(value)` 와 같은 코드를 작성하여 변환할 의사를 명확하게 표현하는 것을 **명시적 변환**이라고 한다. `JavaScript`는 동적 타입 언어이므로 값을 자동으로 여러 유형간에 변환을 자동으로 한다. 이것을 **암묵적 변환** 이라고 한다.

암묵적 변환을 하지 않는 연산자는 `===` 이며, 완전 항등 연산자 라고 한다. 반면에 느슨한 항등 연산자 `==` 는 필요하다면 비교와 타입 강제 변환을 수행한다.

### String 변환

```js
String(123) // 명시적
123 + ''    // 암시적
```
```js
String(123)                   // '123'
String(-12.3)                 // '-12.3'
String(null)                  // 'null'
String(undefined)             // 'undefined'
String(true)                  // 'true'
String(false)                 // 'false'
```

`Symbol` 변환은 명시적으로만 변환될 수 있고, **암시적 변환은 되지 않는다**. 
```js
String(Symbol('my symbol'))   // 'Symbol(my symbol)'
'' + Symbol('my symbol')      // TypeError is thrown
```

### Boolean 변환

```js
Boolean(2)          // 명시적
if (2) { ... }      // 논리적 문맥 때문에 암시적
!!2                 // 논리적 문맥 때문에 암시적
2 || 'hello'        // 논리적 문맥 때문에 암시적
```

논리 연산자(예 : `||` 및 `&&` )에 따른 Boolean 변환을 내부적으로 수행하지만 Boolean값이 아니더라도 원래 피연산자의 값을 실제로 반환한다. 
```js
// true를 반환하는 것이 아닌 123를 반환하고 있다.
// 'hello' and 123 은 표현식을 계산하기 위해서 Boolean으로 강제 변환을 한다.
let x = 'hello' && 123;   // 123
```

```js
Boolean('')           // false
Boolean(0)            // false     
Boolean(-0)           // false
Boolean(NaN)          // false
Boolean(null)         // false
Boolean(undefined)    // false
Boolean(false)        // false
```

`object`, `function`, `Array`, `Date`, 사용자 정의 유형등은 `true` 로 변환한다.
```js
Boolean({})             // true
Boolean([])             // true
Boolean(Symbol())       // true
!!Symbol()              // true
Boolean(function() {})  // true
```

### Numeric 변환
`Number()` 함수를 사용하면 된다. 암시적 변환은 많은 경우에서 작동이 되기 때문에 까다롭다.

```js
Number('123')   // 명시적 - 123
+'123'          // 암시적 - 123
123 != '456'    // 암시적 - true
4 > '5'         // 암시적 - false
5 / null        // 암시적 - Infinity
true | 0        // 암시적 - 1
```

```js
Number(null) // 0
Number(undefined) // NaN
Number(true)  // 1
Number(false) // 0
Number(" 12 ") // 12
Number("-12.34") // -12.34
Number("\n") // 0
Number(" 12s ") // NaN
Number(123) // 123
```
- 문자열을 숫자로 변환할 때 엔진은 먼저 앞뒤의 공백, `\ n`, `\ t` 문자를 제거하고, 문자열이 유효한 숫자를 나타내지 않으면 `NaN` 을 반환한다. **`string`이 비어 있으면 `0`을 반환**한다.
- null와 undefined는 다르게 처리가 되는데 null은 0으로 undefined는 NaN으로 된다.

`Symbol`은 명시적 또는 암시적으로 숫자로 변환될 수 없다. 또한 `TypeError`는 `undefined`로 발생하는 것처럼 `NaN`으로 자동 변환하는 대신 `throw` 된다.
```js
Number(Symbol('my symbol'))    // TypeError is thrown
+Symbol('123')                 // TypeError is thrown
```

#### Tips

- `==` 를 `null` 또는 `undefined` 에 적용하면 숫자 변환이 발생하지 않는다. `null` 은 `null`, `undefined` 와 동일하다.
```js
null == 0 // false, null is not converted to 0
null == null // true
undefined == undefined // true
null == undefined // true
null === undefined // false
```
- `NaN`은 그 자체가 동등하지 않다.
```js
var value = NaN;
if (value !== value) { console.log("we're dealing with NaN here") }
```

<br/>

---

#### 🙏 Reference

- [ImD/Dev-Docs - javascript Type](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/B_Type.md)

