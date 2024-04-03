## react-query 데이터 상태

**fresh**

- staleTime이 지나지 않은 데이터
- 이러한 상태의 데이터를 다시 요청하면, 이 데이터를 그대로 반환한다.

**fetching**

- 데이터를 불러오는 중인 상태
- 서버에 API를 날리고 기다리는 중이라고 보면 될 것 같다.

**stale**

- staleTime이 지난 데이터
- 이러한 상태의 데이터를 다시 요청하면, 서버에 api를 다시 요청한다.

**inactive**

- 쿼리가 실행된 컴포넌트가 unmount 됐을 때, 해당 컴포넌트에서 불러와졌던 데이터들은 inactive상태가 된다 → 사용되지는 않지만 캐싱이 되어 있는 상태(메모리에 남아 있는 상태)

**delete**

- cacheTime이 지나서 아예 삭제된 상태. inactive한 데이터가 cacheTime이 지나면 가비지 컬렉터에 의해 메모리에서 아예 제거된다.

## 캐싱 과정

**query status**

는 실제로 받아 온 data 값이 있는지 없는지를 나타내는 상태 값. → pending, error, success

**fetch status** 는

queryFn() 함수가 현재 실행되는 중인지 아닌지를 나타낸다. → fetching, idle, paused

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0e258c4f-23fc-499c-809b-ffd6fc64b9de/02decbe1-7642-4c7b-a7c3-fb64c8d0973f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0e258c4f-23fc-499c-809b-ffd6fc64b9de/a3bfb740-623d-43d2-b035-adc9b04d2c69/Untitled.png)

- fresh한 데이터를 조회하면, 기존의 데이터를 그냥 보여준다.
- stale한 데이터를 요청하면, 서버에 다시 요청해서 데이터를 가져온다.
- fresh한 상태를 유지하는 시간이 `staleTime`이다.
- stale한 데이터를 요청하면 서버에서 다시 데이터를 가져오는데, 가져오는 동안 캐싱이 된 데이터가 있다면 그 데이터를 보여준다.
- 현재 쿼리 함수가 실행되는 중일 때에는 fetching 상태
- 쿼리 함수가 시작은 했는데 실제로 실행되고 있지 않다면 paused 상태대표적으로 네트워크가 오프라인이 된 경우 기본적으로 paused 상태 됨
- 쿼리 함수가 어떤 작업도 하지 않은 상황이라면(위 두가지 상태도 아닐 때) idle 상태가 됨

## 라이프사이클

- A 쿼리 인스턴스가 mount 됨
- 네트워크에서 데이터 fetch 하고 A라는 query key로 캐싱함
- 이 데이터는 `fresh` 상태에서 `staleTime`(기본값 0) 이후 `stale` 상태로 변경됨
- A 쿼리 인스턴스가 unmount 됨
- 캐시는 `cacheTime`(기본값 5min) 만큼 유지되다가 가비지 콜렉터로 수집됨
- 만일 `cacheTime`이 지나기 전에 A 쿼리 인스턴스가 새롭게 mount되면, fetch가 실행되고 `fresh`한 값을 가져오는 동안 캐시 데이터를 보여줌

## 퀴즈

틀린 문항 찾기

1. 리액트 쿼리에서는 query status와 fetch status 두 가지 상태가 있다. 
2. Query status가 pending일 때 fetch status도 항상 fetching 상태가 된다. 
3. 데이터는 쿼리 키를 이용해서 캐시에 저장 된다. 
4. 처음 서버에서 데이터를 받아왔을 때는 언제나 fresh 상태이다. 
5. useQuery()가 실행되면 항상 쿼리 함수가 실행되어 데이터를 refetch 한다. 
- 정답
    
    2, 4, 5
    
    - 2 - 항상 fetching → paused 상태가 될 수 있음
    - 4 - 처음 서버에서 데이터를 받아오면 staleTime이 0이 되므로 stale 상태이다. ( default 0 )
    - 5 - 데이터가 stale일때만 데이터를 refetch 시킨다.

## 참고

[[React-Query] Query Status, Fetch Status](https://velog.io/@muscatcola/React-Query-Query-Status-Fetch-Status)

[React Query에서 staleTime과 cacheTime의 차이](https://velog.io/@yrnana/React-Query에서-staleTime과-cacheTime의-차이)