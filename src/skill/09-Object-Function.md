## Object.keys(), Object.values(), Object.entries() 그리고 for...in

### Object.keys(), Object.values(), Object.entries()

```js
const developer = {
  name : 'BKJang',
  age : 26,
  lang: 'Korean'
}

console.log(Object.keys(developer)); // ["name", "age", "lang"]
console.log(Object.values(developer)); // ["BKJang", 26, "Korean"]
console.log(Object.entries(developer)); 
/**
0: ["name", "BKJang"]
1: ["age", 26]
2: ["lang", "Korean"]
*/
```

### for...in

```js
const developer = {
  name : 'BKJang',
  age : 26,
  lang: 'Korean'
}

for(let key in developer) {
  console.log(`${key} : ${developer[key]}`);
}
/**
name : BKJang
age : 26
lang: 'Korean'
*/
```