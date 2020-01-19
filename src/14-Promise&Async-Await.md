## Promise와 async-await

### Promise

이전에는 비동기 작업을 처리 할 때에는 콜백 함수로 처리를 해야 했다. 콜백 함수로 처리를 하게 된다면 비동기 작업이 많아질 경우 코드의 가독성이 떨어지게 되었다. 이를 **콜백 지옥**이라고 한다.

Promise는 이러한 콜백 지옥에서 탈출하기 위해 `ES6`에서 도입된 문법이다.

```js
const printNumber = number => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const value = number + 1;
      if (value === 4) {
        const error = new Error("This is Error!");
        reject(error);
        return;
      }
      console.log(value);
      resolve(value);
    }, 1000);
  });
};

printNumber(0)
  .then(n => {
    return printNumber(n);
  })
  .then(n => {
    return printNumber(n);
  })
  .then(n => {
    return printNumber(n);
  })
  .then(n => {
    return printNumber(n);
  })
  .catch(error => {
    console.log(error);
  });
```

`Promise`에서는 `resolve`와 `reject`를 파라미터로 전달하고 성공시에는 `resolve`를 실패시에는 `reject`를 실행한다. 다만, `Promise`를 사용했을 때는 어떤 부분에서 `error`를 잡아야할지가 조금 애매할 수 있고 조건 분기를 해줄 때 불편함이 있다. 이러한 점을 보완한 것이 `async-await` 문법이다.

### Promise.all()

`Promise.all()`은 여러 개의 비동기적 처리를 한 번에 처리하고 싶을 때 사용한다. 단, 모든 비동기 함수가 처리가 완료되면 결과를 출력한다. 따라서 비동기 함수 중 하나라도 에러가 발생한다면 결과 값은 에러가 된다.

```js
const myPromise = time => {
  return new Promise(resolve => setTimeout(resolve, time));
};

const printHello = async () => {
  await myPromise(100);
  return "Hello";
};

const printName = async () => {
  await myPromise(500);
  return "BKJang";
};

const printWorld = async () => {
  await myPromise(300);
  return "world";
};

const printError = async () => {
  await myPromise(600);
  throw new Error("This is Error!");
};

const makeProcess = async () => {
  try {
    const result = await Promise.all([printHello(), printName(), printWorld()]);
    console.log(result);
  } catch (error) {
    console.error(error);
  }
};

const makeProcessWithError = async () => {
  try {
    const result = await Promise.all([
      printHello(),
      printName(),
      printWorld(),
      printError()
    ]);
    console.log(result);
  } catch (error) {
    console.error(error);
  }
};

makeProcess(); //['Hello', 'BKJang', 'world']
makeProcessWithError(); //Error : This is Error!
```

### Promise.race()

`Promise.race()`도 `Promise.all()`과 마찬가지로 모든 비동기 함수를 동시에 요청하지만 가장 먼저 처리된 비동기 함수의 결과만을 반환한다.

```js
const myPromise = time => {
  return new Promise(resolve => setTimeout(resolve, time));
};

const printHello = async () => {
  await myPromise(100);
  return "Hello";
};

const printName = async () => {
  await myPromise(500);
  return "BKJang";
};

const printWorld = async () => {
  await myPromise(300);
  return "world";
};

const printError = async () => {
  await myPromise(600);
  throw new Error("This is Error!");
};

const makeProcessWithError = async () => {
  try {
    const result = await Promise.race([
      printHello(),
      printName(),
      printWorld(),
      printError()
    ]);
    console.log(result);
  } catch (error) {
    console.error(error);
  }
};

makeProcessWithError(); //Hello
```

위의 코드를 보면 에러를 발생시키는 비동기 함수가 `printHello`함수보다 늦게 처리되기 때문에 에러가 아닌 `Hello`가 출력되는 것을 볼 수 있다.

### async-await

`async-await`문법은 `ES8`에서 새롭게 도입된 문법으로 `Promise`를 좀 더 편하게 다룰 수 있게 해준다. 또한 `try-catch`구문을 사용할 수 있기 때문에 에러 처리도 좀 더 간편하게 할 수 있다.

```js
const printNumber = number => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const value = number + 1;
      if (value === 4) {
        const error = new Error("This is Error!");
        reject(error);
        return;
      }
      console.log(value);
      resolve(value);
    }, 1000);
  });
};

const makeProcess = async () => {
  try {
    const num1 = await printNumber(0);
    const num2 = await printNumber(num1);
    const num3 = await printNumber(num2);
    const num4 = await printNumber(num3);
  } catch (error) {
    console.error(error);
  }
};
makeProcess();
```

---

#### 🙏 Reference

- [MDN Docs - Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Captain Pangyo - 자바스크립트 Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)
- [bono's blog - [javascript] async, await를 사용하여 비동기 javascript를 동기식으로 만들자](https://blueshw.github.io/2018/02/27/async-await/)
- [MDN Docs - async function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function)
- [Im-D/Dev-Docs - Promise1](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/Promise1.md)
- [Im-D/Dev-Docs - Promise2](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/Promise2.md)
- [Im-D/Dev-Docs - Promise Pattern](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/PromisePattern.md)
