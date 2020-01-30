## document.createDocumentFragment()

`DocumentFragment`를 활용하는 것은 `reflow`를 줄이기 위한 방법 중 하나다.

```html
<body>
	<select id="timer">
    </select>
</body>
```

```js
function addElements() {
    var target = document.getElementById('timer');
 
    for (var i = 0; i < 24; i++) {
        var option = document.createElement('option');
 
        option.innerText = i;
        target.appendChild(option);
    }
}
```

위 코드는 0시부터 23시까지의 `option`엘리먼트를 셀렉트 박스에 추가하는 예제이다.

`timer`셀렉트박스에 0부터 23까지 반복을 돌려 매번 셀렉트 박스에 엘리먼트를 추가하고 있다. 24번의 DOM 레이아웃 변경이 일어나게 되기 때문에 24번의 `reflow`와 `repaint`가 각각 일어나게 된다.

`DocumentFragment`를 활용했을 때의 가장 큰 차이는 `DocumentFragment`객체는 활성화된 DOM트리의 일부가 아니기 때문에 `DocumentFragment`객체에서 일어나는 변경사항은 DOM에 영향을 주지 않는다. 즉, `reflow`를 일으키지 않으며 성능에 큰 영향을 미치지 않게 된다.

```js
function addElements() {
    var target = document.getElementById('timer');
    var docFrag = document.createDocumentFragment();
    for (var i = 0; i < 24; i++) {
        var option = document.createElement('option');
 
        option.innerText = i;
        docFrag.appendChild(option);
    }

    target.appendChild(docFrag.cloneNode(true));
}
```

위의 코드를 보면 DOM레이아웃을 변경시키는 경우는 `timer`셀렉트 박스 엘리먼트에 추가할 때 발생한다. 즉, `DocumentFragMent`객체를 셀렉트 박스 엘리먼트에 추가할 때 1번만 DOM 레이아웃이 변경된다. 따라서 각각 24번의 `reflow`와 `repaint`가 일어나던 것을 1번씩만 일어나도록 줄일 수 있게 된다.

최신 브라우저의 경우에는 `reflow`가 발생하지 않도록 엔진을 최적화하기 때문에 `DocumentFragment`를 통한 성능 향상을 체감할 수 없는 경우가 많다. 그러나 DOM 객체에 대한 다수의 접근을 필요로하는 작업을 수행해야하는 상황에서는 충분한 성능 향상을 체감할 수 있다.

---

#### 🙏  Reference

- [MDN Docs - Document​Fragment](https://developer.mozilla.org/ko/docs/Web/API/DocumentFragment)
- [DocumentFragment를 이용한 JavaScript 성능 최적화](https://untitledtblog.tistory.com/44)