## 개선에 대한 기준

- 하나의 컴포넌트는 하나의 역할
- 어떤 요소를 보여줄 건진, 사용자가 결정한다.

⇒ 단일책임원칙, 의존성 주입

### **1) SRP : 하나의 컴포넌트에서는 하나의 역할만 감당해야 한다.**

“하나의 모듈은 하나의 역할만 감당해야 한다.” ←→ 하나의 모듈에서 변경이 발생하는 이유는 단 하나여야한다.

변경사항이 있으면 다른 컴포넌트도 수정해야 함 → SRP를 어기고 있다!

→ 각각의 영역을 구분하는 컴포넌트를 분리해야 함 → 각 영역의 변경 사항이 있으면 그 변경은 그 해당 모듈에서만 발생해야 한다!

### **2) DI : 어떤 요소를 보여줄 것인지는 사용할 쪽에서 결정한다. (if문을 제거한다.)**

의존성? 해당 모듈을 사용하기 위해 필요한 것

```jsx
import Logo from "./Logo" // 의존성.

const Navigation => () => {
	return
  	(
      <Container>
	      <Logo>
      </Container>
    )}
```

→ `Navigation` 컴포넌트는 `Logo` 컴포넌트에 대한 의존성이 있다. `Navigation` 컴포넌트가 동작하기 위해서 `Logo` 컴포넌트가 필요하다고 명시하고 있다.

> DI라는 것을 구현한 방식, 즉 의존성을 사용하는 쪽에서 입력하는 방식은 어떤 모습일까?
> 

```jsx
// Navigation.jsx

interface Props {
 children : React.ReactNode;
}

const Navigation => ({ children } : Props) => {
	return (
      <Container>
      	{children}
      </Container>
)}

// app.jsx
import Navigation from "./Navigation"
import Logo from "./Logo"

const App = () => {
	return (
      <Navigation>
	      <Logo>
      </Navigation>
)}
```

→  `Navigation` 컴포넌트 안쪽에서 `Logo` 컴포넌트에 대해 구체적으로 의존하고 있던 의존성이 사라졌다.

이제 무엇이 입력될지는 모르겠지만, `children`이라는 어떤 타입의 컴포넌트가 들어오겠구나 라고 알 수 있음

<aside>
💡 그리고 `Navigation` 컴포넌트를 **사용하는 쪽에서** `Logo` 컴포넌트를 넣어주고 있습니다. **사용하는 쪽에서 의존성을 입력하는 방식**

</aside>

모듈 내부에서 의존성을 가지고 있는 방식을 우리는 **컴파일 타임 의존성이 있다.**

그리고 DI가 적용된, 사용하는 쪽에서 의존성을 주입하는 방식을 우리는 **런타임 의존성** 이 있다고 부른다.

## 더 자세한 내용

[react 공용 컴포넌트 설계하는법(feat.네비게이션바)](https://velog.io/@yesbb/네비게이션바를-설계하는-더-나은-방법)