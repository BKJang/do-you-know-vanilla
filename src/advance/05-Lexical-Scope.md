## 렉시컬 스코프(Lexical Scope)

자바스크립트는 렉시컬 스코프를 지원한다.

우선적으로, 자바스크립트 엔진에서 코드를 컴파일 하는 과정을 보면 다음과 같다.

> * **토크나이징/렉싱** - 코드를 잘게 나누어 토큰으로 만든다.
> * **파싱** - 나눈 토큰을 의미있게 AST(Abstract Syntax Tree)라는 트리로 만든다.
> * **코드생성** - AST를 기계어로 만든다.

렉시컬 스코프란 1단계에서 발생하는 즉, 렉싱 과정에서 정의되는 스코프를 말한다. 
**프로그래머가 변수와 스코프 블록을 어떻게 구성하는냐에 따라 렉싱 타임에서 정의되는 스코프를 렉시컬 스코프**라고 한다.

```javascript
var x = 'global'

function test1() {
    var x = 'local';
    test2();
}

function test2() {
   console.log(x);
}

test1(); //global
test2(); //global
```

위의 코드에서 `test2()`함수를 **어디서 호출하는지가 아닌 어디에 선언되어있냐에 집중**할 필요가 있다.

즉, **`test2()`함수의 상위 스코프는 test1()과 전역이 아닌 전역**이다. 이에 따라 `test2()`에서 출력한 값은 `global`이 나올 것이다.

쉽게 말하면, **렉시컬 스코프는 함수를 어디서 호출하는지가 아닌 어디서 선언했는지에 따라 결정**된다. 이러한 특성때문에 **정적 스코프(Static Scope)** 라고도 한다.

---

#### 🙏 Reference

- [Im-D/Dev-Docs - 렉시컬 속이기(eval)](https://github.com/Im-D/Dev-Docs/blob/master/Javascript/%EB%A0%89%EC%8B%9C%EC%BB%AC_%EC%86%8D%EC%9D%B4%EA%B8%B0(eval).md)