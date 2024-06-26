## 제어 컴포넌트

**React에 의해 값이 제어되는 폼 엘리먼트** 

> 제어 컴포넌트는 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트한다.
> 

 React에서는 변경할 수 있는 state가 일반적으로 컴포넌트의 state 속성에 유지되며 setState()에 의해 업데이트

```jsx
export default function App() {
  const [input, setInput] = useState(""); 
  const onChange = (e) => {
    setInput(e.target.value);
  };

  return (
    <div className="App">
      <input onChange={onChange} />
    </div>
  );
}
```

사용자의 입력을 받는 컴포넌트에 event 객체를 이용해 `setState()`로 값을 저장하는 방식을 제어 컴포넌트 방식이라 할 수 있다.

## 비제어 컴포넌트

> 비제어 컴포넌트는 제어 컴포넌트와는 달리 `setState()`를 쓰지 않고 `ref`를 사용해서 값을 얻는다.
> 

```jsx
export default function App() {
  const inputRef = useRef(); // ref 사용
  const onClick = () => {
    console.log(inputRef.current.value);
  };

  return (
    <div className="App">
      <input ref={inputRef} />
      <button type="submit" onClick={onClick}>
        전송
      </button>
    </div>);
}
```

→ 비제어 컴포넌트는 값이 실시간으로 동기화 X
만약 a와 b라는 컴포넌트가 있을 때, a에 대한 변화를 즉각적으로 b가 영향을 받아야 할때 비제어 컴포넌트는 이런 방식에 대한 대응을 할 수 없다.

제어 컴포넌트의 경우 사용자가 입력을 하는 액션을 취할때마다 리렌더링을 발생시키는 반면, 비제어 컴포넌트는 사용자가 직접 트리거 하기 전까지는 리렌더링을 발생시키지도 않고 값을 동기화 시키지도 않는다.

## 제어 컴포넌트는 언제 사용 하나요?

> 항상 제어 컴포넌트가 옳지 않기 때문에 개발자 역량과 유연한 사고 방식에 따라서 결정,,
> 
- 유효성 검사
- 유효한 데이터가 없는 경우 전송 버튼의 상태를 disabled로 표시하기
- 신용카드와 같은 특정 입력 방식 적용하기

→ 불필요한 단어 입력시에도 값이 갱신 됨

→ 불필요한 리렌더링과 api 호출할 수 있음!

### 제어 컴포넌트는 되고 비제어 컴포넌트는 안 되는 것들

| 기능 | 제어 컴포넌트 | 비제어 컴포넌트 |
| --- | --- | --- |
| 일회성 정보 검색 (예: 제출) | O | O |
| 제출 시 값 검증 | O | O |
| 실시간으로 필드값의 유효성 검사 | O | X |
| 조건부로 제출 버튼 비활성화 (disabled) | O | X |
| 실시간으로 입력 형식 적용하기 (숫자만 가능하게 등) | O | X |
| 동적 입력 | O | X |
- 즉각적으로, 실시간으로 값에 대한 피드백이 필요하다 === 제어 컴포넌트 사용
- 즉각적인 피드백이 불필요하고 제출시에만 값이 필요하다, 불필요한 렌더링과 값 동기화가 싫다 === 비제어 컴포넌트 사용

## 정리

<aside>
📎 state, ref의 렌더링 과정만 알면 쉽게 구별할 수 있을 듯!

</aside>

- **제어 컴포넌트**
    - 제어 컴포넌트의 값은 **항상 최신값**을 유지한다.
    - 새로운 입력 값이 생길때 마다 상태를 새롭게 갱신한다.
    - 데이터와 UI에서 입력한 값이 항상 동기화됨을 알 수 있다.
- **비제어 컴포넌트**
    - 필드에서 값을 트리거 해야 값을 얻을 수 있다.
    - 최종 제출 버튼을 클릭하면 상태를 새롭게 갱신한다.
    - 최종 제출 버튼을 클릭해 트리거 하기 전까지의 값은 변경되지 않는다.