## repaint와 reflow

![rendering](https://github.com/Im-D/Dev-Docs/raw/master/assets/images/rendering.png)

위의 그림과 같이 브라우저는 화면을 rendering하는 과정에서 **배치\(flow\)** 와 **그리기\(paint\)** 의 과정을 거친다.

생성된 DOM 노드의 레이아웃이 변경될 떄, 변경 후 영향을 받는 모든 노드를 다시 계산하고 렌더 트리를 재생성 한다.
이러한 과정을 `reflow`라 하고 `reflow`가 일어난 후, `repaint`가 일어난다.

즉, **DOM의 노드가 변경될 때 마다 DOM tree라는 자료구조에 접근**해야 하기 때문에 DOM의 레이아웃을 변경하는 코드를 작성할 때는 이를 최적화하기 위한 고민이 필요하다.

### reflow

```js
function reFlow() {
    var container = document.getElementById('container');

    container.appendChild(document.createTextNode('hello'));
}
```

위의 코드를 보면 `conatiner`라는 엘리먼트에 `hello`라는 `TextNode`를 추가했다. 이로 인해 DOM 노드의 레이아웃이 바뀌며 `reflow`와 `repaint`가 일어날 것이다.

### repaint

```js
function repaint() {
    var container = document.getElementById('container');

    container.style.backgroundColor = 'black';
    container.style.color = 'white';
}
```

위의 코드에서는 이전의 코드와 다르게 엘리먼트의 `style`만 변경했다. 이러한 경우 DOM 노드의 레이아웃은 변경되지 않았고 `style`속성만 변경되었기 때문에 `reflow`는 일어나지 않고 `repaint`만 일어나게 된다.

`reflow`와 `repaint`가 많아질수록 애플리케이션의 렌더링 성능은 느려지게 되기 때문에 이를 줄일 수록 성능을 높일 수 있다.

---

#### 🙏  Reference

- [Im-D/Dev-Docs - Refaint와 Reflow](https://github.com/Im-D/Dev-Docs/blob/master/Performance/Repaint%EC%99%80%20Reflow.md)
- [Reflow or Repaint(or ReDraw)과정 설명 및 최적화 방법](http://webclub.tistory.com/346)
- [DOM의 문제점과 Virtual DOM](https://velopert.com/775)