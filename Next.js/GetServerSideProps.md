## GerServerSideProps 특징

- SSR 형식
- 서버에서만 실행되고 브라우저에선 실행 되지 않음
- 페이지 요청마다 실행하며 동적으로 데이터를 가져와 업데이트 함
- 외부 데이터를 서버에서 받아와 초기 데이터로 설정하고 서버에게 전달

## 언제 사용할까?

- 동적인 데이터가 필요한 경우
    
    → 사용자의 로그인 상태, 쇼핑카드 내용등과 같이 페이지가 랜더링 될 때마다 바뀌는 데이터가 있는 경우
    
- SEO를 고려하는 경우
    
    → 서버측에서 데이터를 미리 가져오므로 검색 엔진이 페이지의 내용을 분석할 때 SEO에 유리함
    
- API를 통해 데이터를 가져오는 경우
    
    → 클라이언트측에서 CORS 문제 발생을 방지할 수 있음
    

## 기본 형태

```jsx
export async function getServerSideProps(context) {
  // 데이터를 가져오는 비동기 함수
  // ...

  return {
    props: {
      // 데이터 객체
      // ...
    }
  }
}

```

- `context` : Next.js에서 제공하는 컨텍스트 객체로 현재 요청 정보와 함께 페이지에 필요한 다양한 데이터를 가져오는데 사용함
- 페이지에서 `getServerSideProps` 함수를 `export`하는 경우 `Next.js`는 `getServerSideProps`가 반환하는 데이터를 사용하여 페이지를 `pre-render`한다.
- 이때 함수는 페이지 요청마다 실행되고 함수가 반환하는 데이터는 페이지 컴포넌트의 `props`로 전달된다.
- `getServerSideProps` 함수에서는 필요한 데이터를 가져온 다음 `props` 객체에 담아 리턴함

## 예제

```jsx
import * as S from "@/styles/year.style";
import DriverCard from "@/components/card/driverCard";
import Axios from "axios";
import Head from "next/head";

export default function Year({ drivers }) {
  return (
    <S.CardContainer>
      <Head>
        <title>{drivers[0].Driver.familyName}</title>
        <meta name="nationality" content={drivers[0].Driver.nationality}></meta>
      </Head>
      {drivers &&
        drivers.map((driver, index) => (
          <DriverCard key={index} driver={driver} />
        ))}
    </S.CardContainer>
  );
}

export async function getServerSideProps(context) {
  const { year } = context.query;
  const apiUrl = `https://ergast.com/api/f1/${year}/driverStandings.json`;
  const res = await Axios.get(apiUrl);
  const data = res.data.MRData.StandingsTable.StandingsLists[0].DriverStandings;
  return {
    props: {
      drivers: data,
    },
  };
}
```

- `getServerSideProps` 생성
- `context.query`를 이용 === next/router의 `useRouter`
- 데이터를 가져온 뒤 `props` 데이터 객체에 담아 리턴
- 메인 컴포넌트에서 `props`로 사용
- `SEO`를 위한 `<HEAD>, <title>, <meta>` 설정

## 📈 Data Fetching : Client-side vs Server-side

### **Client Side**

- 데이터를 pre-render할 필요가 없고 페이지에 자주 업데이트되는 데이터가 포함되어 있다면 client side에서 데이터를 가져오는 것이 좋음
- 예를 들어 사용자 대시보드 페이지는 사용자별 비공개 페이지이기 때문에 SEO와 관련이 없고, 데이터를 pre-render할 필요도 없고, 데이터가 자주 업데이트 된다. 그래서 client side에서 사용자 데이터를 가져오는 것이 적합함

### **Server Side**

- 하지만 request time에 반드시 데이터를 fetch해야 하는 페이지를 pre-render해야 하는 경우라면 getServerSideProps를 이용하면 좋음

→ 쇼핑몰, 게시판, 영화 정보 등등 서비스

---

[[NextJS] getServerSideProps](https://velog.io/@eunnbi/NextJS-getServerSideProps)

[Next.js SSR, getServerSideProps 사용하기](https://velog.io/@bwj0509/Next.js-SSR-getServerSideProps-사용하기)