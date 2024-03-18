# Intersection Observer API는 무엇이며, 어떤 경우에 사용되나요?

## 기존 스크롤 문제점

`addEventListener()`의 `scroll` 이벤트를 이용해서 무한 스크롤을 구현할 수 있지만, reflow 등의 성능 문제가 발생

→ 무한 스레드,, 이벤트가 단기간에 동기적으로 실행돼서 이벤트가 끊임없이 호출 됨

## **Intersection Observer API**

- Intersection observer는 브라우저 뷰포트와 원하는 요소의 교차점을 관찰하며, 요소가 뷰포트에 포함되는지 아닌지 구별하는 기능을 제공함
- `new IntersectionObserver(callback, options)` 방식으로 관찰자를 초기화하고, 관찰할 대상을 지정할 수 있음.
- `boundingClientRect` 등의 메서드를 사용하면, reflow를 일으키지 않고 관찰 대상의 경계를 계산할 수 있음

→ 무한 스크롤 구현할 때 사용하면 좋음

## 사용 때?

- 페이지가 스크롤 되는 도중에 발생하는 이미지나 다른 컨텐츠의 지연 로딩 (lazy loading).
- 스크롤 시에, 더 많은 컨텐츠가 로드 및 렌더링되어 사용자가 페이지를 이동하지 않아도 되게 하는 infinite-scroll 을 구현.
- 광고 수익을 계산하기 위한 용도로 광고의 가시성 보고.
- 사용자에게 결과가 표시되는 여부에 따라 작업이나 애니메이션을 수행할 지 여부를 결정.