## Deep Copy

*use `JSON.parse` , `JSON.stringify`*
```js
function changeAgePure(person) {
    var newPersonObj = JSON.parse(JSON.stringify(person));
    newPersonObj.age = 25;
    return newPersonObj;
}
    
var alex = {
    name: 'Alex',
    age: 30
};
var alexChanged = changeAgePure(alex);

console.log(alex); // -> { name: 'Alex', age: 30 }
console.log(alexChanged); // -> { name: 'Alex', age: 25 }
```

**or** *use `$.extend()`*
```js
function changeAgePure(person) {
    var newPersonObj = $.extend(true, {}, person);
    newPersonObj.age = 25;
    return newPersonObj
}
    
var alex = {
    name: 'Alex',
    age: 30
};
var alexChanged = changeAgePure(alex);

console.log(alex); // -> { name: 'Alex', age: 30 }
console.log(alexChanged); // -> { name: 'Alex', age: 25 }
```

**or** *use `destructuring`* (ES6)
```js
function changeAgePure(person) {
    var newPersonObj = { ...person };
	newPersonObj.age = 25;
	return newPersonObj
}
    
var alex = {
    name: 'Alex',
    age: 30
};
var alexChanged = changeAgePure(alex);

console.log(alex); // -> { name: 'Alex', age: 30 }
console.log(alexChanged); // -> { name: 'Alex', age: 25 }
```

---

#### 🙏 Reference

- [ImD/Dev-Docs - javascript Type](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/B_Type.md)