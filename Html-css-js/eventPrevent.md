`event.preventDefault()` 와 `event.stopPropagation()` 는 두 메서드 모두 이벤트를 중단시킨다.

## **Q1. event.preventDefault란 무엇이며 언제 사용하는가**

`e.preventDefault()` 는 html에서 표준으로 제공하는 태그의 기본 이벤트를 막는 것이다.

`<a>` , `<submit>` , `<button>` 와 같은 몇몇 태그들은 특수한 기능인 해당 페이지를 새로고침 하는 기능을 가지고 있는데, 이때 `e.preventDefault()` 를 통해 이벤트 발생을 막을 수 있다.

## **Q2. event.preventDefault는 어떻게 사용할까**

`event.preventDefault()` 는 `<a>`와 `<submit>`와 같은 몇몇 태그의 고유의 동작을 중단시킨다.

> `<a>` 에 `event.preventDefault()` 사용 → 태그에 링크 값이 있어도 `event.preventDefault()` 로 인해 클릭 시 이동하지 않는다.
> 

> `<submit>` 에 `event.preventDefault()` 사용 → `<submit>` 태그를 클릭해도 `event.preventDefault()` 로 인해 제출 후 새로고침되지 않는다.
> 

## **Q3. 그럼 event.stopPropagation은 무엇일까?**

**`event.stopPropagation()` 는** 상위 엘리먼트로의 이벤트 전파(이벤트 버블링)을 막기 위한 메서드이다.

js에서 이벤트가 전파되어 상위 엘리먼트에서 발생한 이벤트가 하위 엘리먼트에서 발생한 이벤트 결과에 원치 않는 결과를 주는 경우 사용한다.

## Q4. 총정리 및 차이점

---

`event.preventDefault()` 는 HTML에서 표준으로 제공하는 태그의 기본 이벤트 발생을 막는 메서드이고, `event.stopPropagation()`는 상위 엘리먼트로의 이벤트 버블링을 막는 메서드이다.

만약 이벤트가 상위 DOM으로 전파되지 않게 하고 싶다면 `event.stopPropagation()` 를 사용하는 것이 적절하다.

➕ **추가**

`event.preventDefault()` : 기본적인 클릭 동작만 막고 + 외부에서 들어온 동작을 직접적으로 막진 않는다.

`event.stopPropagation()` : 링크나 버튼의 클릭을 막진 못하고 + 상위 태그까지의 전파를 막는다.