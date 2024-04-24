## **[1. What are Server Components](https://html-jc.tistory.com/657#1.%20What%20are%20Server%20Components-1)**

<aside>
💡 **Server Components?** → 애플리케이션의 서버 부분에서 렌더링되는 컴포넌트

</aside>

이는 대부분의 컴포넌트가 서버에서 렌더링되고, 작은  UI 요소만 클라이언트에서 렌더링 되는 방식.

그리고 이 작은 인터랙티브 UI요소들을 클라이언트 컴포넌트라고 지칭할 수 있다.

<aside>
💡 **Client Components? →** 클라이언트 측에서 렌더링되는 컴포넌트

</aside>

이 컴포넌트는 사용자와의 상호작용을 담당하며, 애플리케이션의 인터랙티브한 부분을 담당한다.

클라이언트 컴포넌트는 Next.js와 같은 프레임워크에서의 서버에서 사전 렌더링되고 클라리언트에서 Hydrate되어 초기 렌더링 성능을 개선할 수 있다.

**Hydrate?** → Server Side 단에서 렌더링 된 정적 페이지와 번들링된 JS파일을 클라이언트에게 보낸 뒤, 클라이언트 단에서 HTML 코드와 React인 JS코드를 서로 매칭 시키는 과정.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/ffb2a6df-f526-46cd-86c5-2cefc149f653/Untitled.png)

### **서버 컴포넌트**와 **서버 사이드 렌더링(SSR)**

- **서버 컴포넌트**의 코드는 클라이언트로 전달되지 않는다. BUT **SSR**의 모든 컴포넌트의 코드는 JS번들에 포함되어 클라이언트로 전송된다.
- **서버 컴포넌트**는 페이지 레벨에 상관없이 모든 컴포넌트에서 서버에 접근 가능하다. BUT Next.js의 경우 가장 top level의 페이지에서만 getServerProps()나 getInitialProps()로 서버에 접근 가능하다.
- **서버 컴포넌트**는 클라이언트 상태를 유지하며 refetch 될 수 있다. **서버 컴포넌트**는 HTML이 아닌 특별한 형태로 컴포넌트를 전달하기 때문에 필요한 경우 포커스, 인풋 입력값 같은 클라이언트 상태를 유지하며 여러 번 데이터를 가져오고 리렌더링하여 전달할 수 있다. BUT **SSR**의 경우 HTML로 전달되기 때문에 새로운 refetch가 필요한 경우 HTML 전체를 리렌더링 해야 하며 이로 인해 클라이언트 상태를 유지할 수 없다.

> **서버 컴포넌트**는 SSR의대체가 아닌 **보완의 수단**으로 사용할 수 있다. **SSR**으로 초기 HTML 페이지를 빠르게 보여주고, **서버 컴포넌트**로는 클라이언트로 전송되는 자바스크립트 번들 사이즈를 감소시킨다면 **사용자에게 기존보다 훨씬 빠르게 인터렉팅한 페이지를 제공할 수 있을 것이다.**
> 

## **[2. Why Server Components?](https://html-jc.tistory.com/657#2.%20Why%20Server%20Components%3F%C2%A0-1)**

Client Components < Server Components?

**1. 서버 컴포넌트를 통해 개발자는 서버 인프라를 더 잘 활용할 수 있다.** 

- 성능 향상
- React의 강력함과 유연성, 그리고 컴포넌트 기반 UI 템플릿 모델을 함께 제공한다

**2. 초기 페이지 로드 속도 증가 및 클라이언트 측 자바스크립트 번들 크기 감소**

**3. Next.js로 라우트가 로드되면 초기 HTML이 서버에서 렌더링된다.**

**4. 서버 컴포넌트로 전환을 쉽게하기 위해 App Router 내의 모든 컴포넌트는 기본적으로 서버 컴포넌트로 지정된다.** 

## **[3. Client Components](https://html-jc.tistory.com/657#3.%20Client%20Components-1)**

```jsx
'use client';
 
import { useState } from 'react';
 
export default function Counter() {
  const [count, setCount] = useState(0);
 
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/d145c634-aa78-4854-901a-707c0c629b31/Untitled.png)

`'use client'` 지시어가  서버 전용 코드와 클라이언트 코드 사이에 있다.

`'use client'` 지시어가 파일에 정의되면 자식 구성 요소를 포함하여 파일로 가져온 다른 모든 모듈은 클라이언트 번들의 일부로 간주된다.

- 클라이언트 컴포넌트 모듈 그래프 내부에 있는 컴포넌트들은 대부분 클라이언트에서 렌더링 되지만 `Next.js`를 사용하면 서버에서 사전 렌더링되고 클라이언트에서 Hydrate될 수도 있다.
- `"use client"` 지시문은 다른 것들을 `import` 하기전에 반드시 파일 제일 상단에 정의되어야 한다.
- 모든 파일에서 `"use client"` 지시문을 정의할 필요는 없다. 클라이언트 모듈 경계는 "진입점"에서 한 번만 정의하면 클라이언트 컴포넌트로 간주되는 모든 모듈을 가져올 수 있다.