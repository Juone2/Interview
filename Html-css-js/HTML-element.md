<aside>
💻 innerHTML은 요소 내에 있는 HTML과 XML 모두를 의미하고,

innerText는 요소 내에서 사용자에게 보여지는 text를 의미하고,

textContent는 script나 style 태그와 상관없이 해당 노드가 가지고 있는 text를 의미한다.

</aside>

## innerHTML

`element`의 속성으로 안에 포함된 HTML이나 XML 마크업을 가져오거나 태그와 함께 입력 및 설정 가능하다.

→ innerHTML을 사용하면 내부 HTML 코드를 js를 사용해서 쉽게 변경 가능하다.

```jsx
// html 코드와 함께 작성 가능
document.documentElement.innerHTML = "<p>innerHTML</p>"
// 스타일 적용
document.documentElement.innerHTML =
  "<span style='color:blue'>innerHTML</span>"

// 이런 식으로 빈 문자열을 넣으면 body의 전체 내용을 지울 수 있다.
document.body.innerHTML = "";
```

## innterText

`element` 의 속성으로 안에 포함된 사용자에게 보여지는 text값을 가져오거나 설정할 수 있다.

```jsx
// innerHTML과 달리 text값만 다루기 때문에 html태그 사용 불가능
document.documentElement.innerText = "innerText"

// html태그를 넣으면 태그도 text값으로 인식하고
// <p>innerText</p> 문자열 그대로 적용함.
document.documentElement.innerText = "<p>innerText</p>"
```

- innerHTML과 innerText 비교

```jsx
const innerT = document.getElementById('innerT');
innerT.innerText = "<div style='color:red'>innerText</div>";
console.log(innerT)
// 스타일 적용되지 않은 기본 폰트로 <div style='color:red'>innerText</div> 출력

const innerH = document.getElementById('innerH');
innerH.innerHTML = "<div style='color:red'>innerHTML</div>";
console.log(innerH)
// 스타일 적용된 빨간색 폰트로 innerHTML 출력
```

## textContent

`node` 속성으로 사용자에게 보여지는 text값만 읽어오는 innterHTML과는 달리 해당 노드가 가지고 있는 텍스트 값을 모두 읽어온다.

### HTML

```html
<div id='content'>
  안녕~
  <span style='display:none'>innerText는 나를 볼 수 없어😏</span></div>
```

### JS

```jsx
const content = document.getElementById('content');

console.log(content.innerHTML);
// html 전체를 다 가져옴

// 안녕~
// <span style='display:none'>innerText는 나를 볼 수 없어😏</span>

-----------------------------------------------------

console.log(content.innerText);
// 사용자에게 보여지는 텍스트만 가져옴
// 숨겨진 텍스트는 사용자에게 보여지지 않기 때문에 안녕~만 가져옴

// 안녕~

-----------------------------------------------------

console.log(content.textContent);
// 숨겨진 텍스트까지 포함해서 텍스트값을 모두 다 가져옴

// 안녕~
// innerText는 나를 볼 수 없어😏
```