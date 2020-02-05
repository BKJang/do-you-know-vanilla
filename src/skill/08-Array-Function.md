## 배열 내장함수

자바스크립트의 배열에서는 기본적으로 많은 종류의 내장 함수를 제공하고 있고 이를 이용하면 보다 간단한 코드로 다양한 기능을 구현할 수 있다.

### forEach

`forEach`는 배열을 반복하여 기존 값을 가져오는데 주로 쓰인다.

```js
const arr = [1, 2, 3, 4, 5];

arr.forEach(item => {
  console.log(item); //1 2 3 4 5
});
```

### map

`map`과 `forEach`의 차이는 배열을 반복하면서 각각의 원소에 대하여 특정 로직을 수행한 뒤, 새로운 배열을 반환하고 싶을 때 주로 사용한다.

```js
const arr = [1, 2, 3, 4, 5];

const newArr = arr.map(item => {
  return item * 2;
});

console.log(arr); //[1, 2, 3, 4, 5]
console.log(newArr); //[2, 4, 6, 8, 10]
```

위에서 볼 수 있듯이 `map`을 통해 반환한 배열은 깊은 복사를 사용하기 때문에 기존 배열을 영향을 주지 않고 새로운 배열을 반환한다.

### filter

`filter`함수의 기능은 이름 그대로 배열을 반복하며 각각의 원소들 중 특정 조건에 해당하는 원소들만 뽑아내어 새로운 배열을 반환한다.
`filter`또한 `map`과 마찬가지로 기존 배열에 영향을 주지 않는다.

```js
const arr = [1, 2, 3, 4, 5];

const newArr = arr.filter(item => {
  return item >= 3;
})

console.log(arr); //[1, 2, 3, 4, 5]
console.log(newArr); //[3, 4, 5]
```

### indexOf

`indexOf`함수는 배열에서 찾고자 하는 원소가 있다면 그 원소의 `index`값을 반환한다.

```js
const arr = ['a', 'b', 'c', 'd'];

console.log(arr.indexOf('c')); //2
```

### findIndex

`findIndex`함수도 `indexOf`함수와 마찬가지로 찾고자 하는 원소의 `index`값을 반환한다. 하지만 원소가 객체로 되어있거나 배열로 되어있을 때 `indexOf`함수로는 `index`값을 찾을 수 없지만 `findIndex` 함수는 조건 처리를 통하여 `index`값을 찾을 수 있다.

```js
const arr = [
  {
    id: 1,
    name: 'BKJang',
    age: 27,
  },
  {
    id: 2,
    name: 'JHKim',
    age: 25,
  }
]

console.log(arr.findIndex(item => item.id === 2)); //1
```

### find

`find`함수는 `findIndex`함수와 사용법은 동일하지만 반환하는 값이 `index`값이 아닌 찾아낸 값 자체를 반환한다.

```js
const arr = [
  {
    id: 1,
    name: 'BKJang',
    age: 27,
  },
  {
    id: 2,
    name: 'JHKim',
    age: 25,
  }
]

console.log(arr.find(item => item.id === 2)); 
// {id: 2, name: "JHKim", age: 25}
```

### splice

`splice`함수의 첫번째 파라미터는 **지우기 시작할 원소의 `index`**, 두번째 파라미터는 **지울 원소의 갯수**를 넘긴다.

```js
const arr = ['a', 'b', 'c', 'd', 'e'];

const arr2 = arr.splice(2, 3);

console.log(arr); //["a", "b"]
console.log(arr2); //["c", "d", "e"]
```

### slice

`slice`함수와 `splice`함수의 가장 큰 차이점은 `slice`함수는 기존 배열에 영향을 주지 않고 새로운 배열을 반환한다는 것이다.<br/>
또 다른 차이점은 `slice`함수는 두번째 파라미터로 보낸 원소의 `index`값 전까지 원소를 제거한다.

```js
const arr = ['a', 'b', 'c', 'd', 'e'];

const arr2 = arr.slice(1, 3);

console.log(arr); //["a", "b", "c", "d", "e"]
console.log(arr2); //["b", "c"]
```

### shift

`shift`함수는 기존 배열의 원소를 앞에서부터 하나씩 제거한다.

```js
const arr = [1, 2, 3, 4, 5];

arr.shift();
console.log(arr); //[2, 3, 4, 5]

arr.shift();
console.log(arr); //[3, 4, 5]
```

### unshift

`unshift`함수는 기존 배열에 새로운 원소를 앞에 추가한다.

```js
const arr = [1, 2, 3, 4, 5];

arr.unshift(0);
console.log(arr); //[0, 1, 2, 3, 4, 5]

arr.unshift(-1);
console.log(arr); //[-1, 0, 1, 2, 3, 4, 5]
```

### push

`push`함수는 기존 배열에 새로운 원소를 뒤에 추가한다.

```js
const arr = [1, 2, 3, 4, 5];

arr.push(6);
console.log(arr); //[1, 2, 3, 4, 5, 6]

arr.push(7);
console.log(arr); //[1, 2, 3, 4, 5, 6, 7]
```

### pop

`pop`함수는 기존 배열의 원소를 뒤에서부터 하나씩 제거한다.

```js
const arr = [1, 2, 3, 4, 5];

arr.pop();
console.log(arr); //[1, 2, 3, 4]

arr.pop();
console.log(arr); //[1, 2, 3]
```

### concat

`concat`은 여러 개의 배열을 하나로 합쳐주는 함수다. 기존 배열들에는 영향을 끼치지 않고 새로운 배열을 반환한다. `ES6`에서는 `concat`대신 `Spread Operator`를 많이 사용한다.

```js
//concat
const arr1 = ['a', 'b'];
const arr2 = ['c', 'd', 'e'];

const newArr = arr1.concat(arr2);

console.log(arr1); //["a", "b"]
console.log(arr2); //["c", "d", "e"]
console.log(newArr); //["a", "b", "c", "d", "e"]
```

```js
//ES6 Spread Operator
const arr1 = ['a', 'b'];
const arr2 = ['c', 'd', 'e'];

const newArr = [...arr1, ...arr2];

console.log(arr1); //["a", "b"]
console.log(arr2); //["c", "d", "e"]
console.log(newArr); //["a", "b", "c", "d", "e"]
```

### join

`join`함수는 배열의 원소들을 합쳐 문자열 형태로 반환한다.

```js
const arr = ['a', 'b', 'c', 'd', 'e'];

console.log(arr.join(', ')); //a, b, c, d, e
console.log(arr.join('')); //abcde
```

### every

`every`함수는 특정 조건에 대하여 배열의 모든 원소가 통과해야만 `true`를 반환하며 빈 배열에 대해서는 무조건 `true`를 반환한다.

```js
const arr = [1, 2, 3, 4, 5];

const result1 = arr.every(item => item <= 5);
const result2 = arr.every(item => item < 3);

console.log(result1, result2); //true false
```

### some

`some`함수는 특정 조건에 대하여 배열의 어떤 한 요소라도 통과하면 `true`를 반환하며 빈 배열에 대해서는 무조건 `false`를 반환한다.

```js
const arr = [1, 2, 3, 4, 5];

const result1 = arr.some(item => item <= 5);
const result2 = arr.some(item => item < 3);

console.log(result1, result2); //true true
```

### sort

```js
const fruit = ['orange', 'apple', 'banana'];

fruit.sort();
console.log(fruit); //["apple", "banana", "orange"]
```

```js
const imD = [
    { name : "BKJang", age : 27},
    { name : "JHKim", age : 25},
    { name : "SHJo", age : 28},
    { name : "DHJung", age : 29},
    { name : "JSKang", age : 23}
]

/* 이름순 */
imD.sort((a, b) => { // 오름차순
    return a.name < b.name ? -1 : a.name > b.name ? 1 : 0;
});
/**
0: {name: "BKJang", age: 27}
1: {name: "DHJung", age: 29}
2: {name: "JHKim", age: 25}
3: {name: "JSKang", age: 23}
4: {name: "SHJo", age: 28}
*/

imD.sort((a, b) => { // 내림차순
    return a.name > b.name ? -1 : a.name < b.name ? 1 : 0;
});
/**
0: {name: "SHJo", age: 28}
1: {name: "JSKang", age: 23}
2: {name: "JHKim", age: 25}
3: {name: "DHJung", age: 29}
4: {name: "BKJang", age: 27}
*/

/* 나이순 */
const sortingField = 'age';

imD.sort((a, b) => { // 오름차순
    return a[sortingField] - b[sortingField];
});
/**
0: {name: "JSKang", age: 23}
1: {name: "JHKim", age: 25}
2: {name: "BKJang", age: 27}
3: {name: "SHJo", age: 28}
4: {name: "DHJung", age: 29} 
*/

imD.sort((a, b) => { // 내림차순
    return b[sortingField] - a[sortingField];
});
/**
0: {name: "DHJung", age: 29}
1: {name: "SHJo", age: 28}
2: {name: "BKJang", age: 27}
3: {name: "JHKim", age: 25}
4: {name: "JSKang", age: 23} 
*/
```

### reduce

`reduce`함수는 누적 값과 현재 값을 이용하여 여러 가지 기능을 구현할 수 있는 매우 유용한 함수다. 사실, `reduce`만 잘 사용할 줄 알아도 `filter`함수의 기능까지도 구현할 수 있다.

```javascript
var arr = [1, 2, 3, 4, 5];

var sum = arr.reduce((acc, cur) => {
  return acc + cur;
});

console.log(sum); // 15
```

```javascript
var arr = [1, 2, 3, 4, 5];
var reducer = (acc, cur) => {
  return acc + cur;
};

var sum = arr.reduce(reducer);

console.log(sum); // 15
```

```javascript
var arr = ['Kim', 'Kim', 'Kang', 'Jang', 'Jo', 'Kang', 'Jo'];

var reducer = (acc, cur, index) => {
  if (!acc[cur]) {
    acc[cur] = 1;
  } else {
    acc[cur] = acc[cur] + 1;
  }

  return acc; // 여기
};

var sorting = arr.reduce(reducer, {});

console.log(sorting); // { Kim: 2, Kang: 2, Jang: 1, Jo: 2 }
```

```javascript
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 15, 16, 20];

var reducer = (acc, cur, index) => {
  if (cur % 2 === 0) acc.push(cur * 2);
  return acc;
};

var double = arr.reduce(reducer, []);

console.log(double);
```

```javascript
const input = [
  {
    title: '슈퍼맨',
    year: '2005',
    cast: ['장동건', '권상우', '이동욱', '차승원']
  },
  {
    title: '스타워즈',
    year: '2013',
    cast: ['차승원', '신해균', '장동건', '김수현']
  },
  {
    title: '고질라',
    year: '1997',
    cast: []
  }
];
const key = 'cast';

const flatMapReducer = (acc, cur) => {
  cur[key].reduce((acc2, cur2) => {
    if (acc2.indexOf(cur2) === -1) acc2.push(cur2);
    return acc2;
  }, acc);

  return acc;
};
const flattenCastArray = input.reduce(flatMapReducer, []);
// ['장동건', '권상우', '이동욱', '차승원', '신해균', '김수현']

console.log(flattenCastArray);
```

### reduceRight

`reduceRight`함수는 기존의 `reduce`와 원리는 동일하지만 `current`에 마지막 `index`원소부터 첫번째 원소 순서로 들어간다. 아래는 배열을 `nested object`로 만드는 예시다.

```js
const makeNestedObjWithArray = (arr) => {
  return arr.reduceRight(
    (accumulator, item) => {
      const newAccumulator = {};
      newAccumulator[item] = Object.assign(
        {},
        accumulator
      );
      return newAccumulator;
    },
    {}
  );
};

const list = ["a", "b", "c"];
const obj = makeNestedObjWithArray(list);
console.log(obj);
/**
a : { b: { c: {} } }
*/
```

---

#### 🙏 Reference

- [MDN Docs - Array.some()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
- [MDN Docs - Array.every()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- [DUDMY HOME - 자바스크립트 정렬 함수, sort()](http://dudmy.net/javascript/2015/11/16/javascript-sort/)
- [비비로그 - 자바스크립트의 유용한 배열 메소드 사용하기... map(), filter(), find(), reduce()](https://bblog.tistory.com/300)
- [Im-D/Dev-Docs - Reduce](https://github.com/Im-D/Dev-Docs/edit/master/Javascript/Reduce.md)
- [How to create nested child objects in Javascript from array?](https://hashnode.com/post/how-to-create-nested-child-objects-in-javascript-from-array-cj9tsc3we01m0uowu4pyuesy0)