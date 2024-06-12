## App Router

`app` 폴더를 기반으로 라우팅을 하기 때문에 앱 라우터라고 불린다. 리액트 서버 컴포넌트 기반으로 구성된 라우터이며 아래의 편의 기능을 제공합니다.

- 공용 레이아웃
- 중첩 라우팅
- 로딩 상태 제어
- 에러 처리

`app` 폴더 안에 컴포넌트 파일을 만들면 이 컴포넌트는 기본적으로 서버 컴포넌트가 된다.

→ `‘use client’` 를 사용하여 클라이언트 컴포넌트 생성 가능

## App Router 파일 컨벤션 및 역할[](https://cracking-next.vercel.app/docs/routing#%EC%95%B1-%EB%9D%BC%EC%9A%B0%ED%84%B0-%ED%8C%8C%EC%9D%BC-%EC%BB%A8%EB%B2%A4%EC%85%98-%EB%B0%8F-%EC%97%AD%ED%95%A0)

앱 라우터 폴더에는 다음 특정 파일들을 생성할 수 있다.

- `layout` : 공통 UI(레이아웃)를 배치하는 컴포넌트
- `page` : 특정 URL에 해당하는 페이지 컴포넌트. `page`라는 이름을 붙이면 해당 URL로 접근 가능
- `loading` : 해당 영역에 대한 로딩 컴포넌트
- `not-found` : 페이지를 찾을 수 없습니다(404)에 해당하는 에러 바운더리 컴포넌트
- `error` : 에러가 발생했을 때 에러 UI를 표시하는 에러 바운더리 컴포넌트
- `global-error` : 전역 에러 UI를 표시하는 에러 처리 컴포넌트
- `route` : API 엔드포인트로 취급되는 파일
- `template`: 레이아웃 컴포넌트가 다시 그려질 때 표시될 UI
- `default` : 병렬 라우팅 처리시 표시할 기본 UI

![파일들의 위계 표현](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/451625f2-2a95-4dbc-9314-0e6f691c73a3/Untitled.png)

파일들의 위계 표현

![라우터 중첩 시키기](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/545cdce3-cd81-4c86-be09-294e8de31237/Untitled.png)

라우터 중첩 시키기

## App Router 장점[](https://cracking-next.vercel.app/docs/routing#%EC%95%B1-%EB%9D%BC%EC%9A%B0%ED%84%B0-%EC%9E%A5%EC%A0%90)

앱 라우터의 장점은 `app` 폴더 밑에 라우터 파일 뿐만 아니라 라우터에서 사용될 파일들을 가까이 배치할 수 있는 장점이 있다.

- 리액트 컴포넌트 파일
- 라이브러리 파일
- API 파일

![페이지 라우터에서 지원 X → `pages` 폴더 안에 들어간 컴포넌트 파일에 대해 모든 라우팅을 구성해주기 때문.](https://prod-files-secure.s3.us-west-2.amazonaws.com/858ac9c3-9dda-4548-9019-2e429c4b0ad0/e48c7c50-5e10-4156-b9ec-7d7a40806f65/Untitled.png)

페이지 라우터에서 지원 X → `pages` 폴더 안에 들어간 컴포넌트 파일에 대해 모든 라우팅을 구성해주기 때문.

## 앱 라우터와 페이지 라우터의 가장 큰 차이점[](https://cracking-next.vercel.app/docs/routing#%EC%95%B1-%EB%9D%BC%EC%9A%B0%ED%84%B0%EC%99%80-%ED%8E%98%EC%9D%B4%EC%A7%80-%EB%9D%BC%EC%9A%B0%ED%84%B0%EC%9D%98-%EA%B0%80%EC%9E%A5-%ED%81%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90)

앱 라우터는 같은 관심사를 최대한 가까이 배치할 수 있게 되었습니다. 페이지 라우터는

- `pages`, `layouts`, `components`, `libs`

등의 폴더가 항상 별도로 구성되어 있어 파일 간에 참조된 코드를 보느라 여기저기 뒤져야 하는 비용이 컸다. 

→ 반면에, 앱 라우터는 `app`이라는 폴더 안에 특정 라우팅과 관계된 페이지 컴포넌트 바로 옆에 필요한 

- `layouts`, `components`, `library` 파일들을 배치할 수 있게 되어 더 파일 배치가 쉬워졌다.
