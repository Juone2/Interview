## 이벤트 버블링

이벤트가 발생한 요소부터 점점 부모 요소를 거슬러 올라가서 window 까지 이벤트를 전파하는 것. 

→ 거의 모든 이벤트는 버블링이 이루어 진다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/60d1c2c6-f7e2-4f94-8547-46586cb0f82e/Untitled.png)

## 버블링 강제로 중단하기

`e.stopPropagation()` 사용 → 추후에 문제가 될 수 있는 상황을 만들 수 있으므로 자주 사용하는 건 지양 하는 게 좋음

## 이벤트 캡쳐링

window 부터 이벤트가 발생한 요소까지 이벤트를 전파하는 것

→ 잘 사용 되지는 않음

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/b9852aa7-0e29-4842-a021-0bf3a0972559/Untitled.png)

## 이벤트 캡쳐링 후 버블링

```jsx
<html>
  <body>
    <!-- 빨간색 -->
    <div class="depth1">
      <!-- 초록색 -->
      <div class="depth2">
      	<!-- 파란색 -->
        <div class="depth3">
          depth3
        </div>
      </div>    
    </div>
  </body>
  
  <script>
  for(let elem of document.querySelectorAll('*')) {
  	elem.addEventListener("click", e => alert(`[캡쳐링] tag: ${elem.tagName}, class: ${elem.className}`), true);
  	elem.addEventListener("click", e => alert(`[버블링] tag: ${elem.tagName}, class: ${elem.className}`));
  }
  </script>
</html>
```

- 코드 설명
    - 이벤트는 document에서 시작해 DOM 트리를 따라 event.target (이벤트가 발생한 가장 안쪽 요소)까지 내려갑니다.
    - 이벤트는 트리를 따라 내려가면서 addEventListener(..., true)로 할당한 핸들러를 동작시킵니다.
    - 이후 타깃 요소(event.target)에 설정된 핸들러가 호출됩니다.
    - 이후엔 이벤트가 event.target부터 시작해서 다시 최상위 노드까지 전달되면서 각 요소에 on<event>로 할당한 핸들러와 addEventListener로 할당한 핸들러를 동작시킵니다. (addEventListener로 할당한 핸들러 중, 세 번째 인수가 없거나 false, {capture: false}인 핸들러만 호출됩니다.)