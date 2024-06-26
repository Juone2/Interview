## 해시란?

key를 value에 매핑하는 array 형태의 자료구조 → key를 hash function에 넣어 얻은 hashes를 index로 value 데이터와 매핑하는 array(table) 형태의 자료구조

## 용어

Hash: key를 value에 매핑하는 array 형태의 자료구조

Hash function: 임의 길이 데이터(input)를 암호화된 고정 길이(output)의 데이터로 매핑(전환)하는 함수

Hashing: 해시 함수에서 Key값을 hash로 변환하는 과정

Hash Collision: 서로 다른 키(key)가 같은 해시(hash)가 되는 경우 → Hash Collision을 최대한 줄이는 것이 중요하다.

## 구조

![스크린샷 2024-02-05 오후 7.26.03.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/0e258c4f-23fc-499c-809b-ffd6fc64b9de/6688ba05-10ad-4664-8267-519816990672/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-02-05_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_7.26.03.png)

- 해시 테이블에서 bucket은 key에 대응하는 데이터이다.
- bucket에 들어가는 데이터는 hash function과는 아무런 상관이 없다.
- key값을 hash func에 넣어 얻은 hash value를 배열의 인덱스로 쓰는 테이블을 hash table이라 칭한다.

## 해시과정

1. 데이터들이 Hash Function의 규칙에 의해 Hash Code를 가지게 된다.
2. Hash Code를 통해 Hash Table 안에 규칙에 의해 들어간다.

→ 1, 2번의 모든 과정이 해싱이 되는 것

## 시간 복잡도

**O(1)의 시간 복잡도를 지향**

1이라는 데이터가 Hash Table 안에 있는지를 확인할 때

1. 1을 Hash Function에 의해 변환
2. Hash Code를 Hash Function을 통해 뽑아내고, Hash Code에 해당하는 index에 1이라는 값이 Hash Table에 있는지 확인

→ O(1)의 시간 복잡도를 가질 수 있음

## 장/단점

### 장점

- key-value가 1:1로 매핑되어 있기 때문에 삽입, 삭제, 검색 과정에서 모두 평균적으로 O(1)의 시간 복잡도를 가지고 있다.

### 단점

- 해시 충돌 발생
- 순서/관계가 있는 배열에 어울리지 않음 (순서에 상관없이 key만을 가지고 삽입/검색/삭제 하기 때문)
- 공간 효율성이 떨어짐 (데이터가 저장되기 전에 미리 저장공간을 확보해야하기 때문. 공간이 부족하거나 아예 채워지지 않는 경우가 발생)
- hash function의 의존도가 높음 (평균 시간 복잡도가 O(1)이지만 해시함수가 매우 복잡하다면 해시 테이블의 연산 속도는 증가)

## 해시 충돌 해결 방안

많은 해시 충돌은 해시테이블의 성능을 떨어뜨림 → 충돌 최소화 필요

### **1) Chaining**

bucket 내에 연결리스트(Linked List)를 할당하여, bucket에 데이터를 삽입하다가 해시 충돌이 발생하면 연결리스트로 데이터들을 연결하는 방식 → 데이터의 주소값은 바뀌지않는다.

연결 리스트만 사용하면 된다. 즉, 복잡한 계산식을 사용할 필요가 개방주소법에 비해 적다. 

리스트를 하나씩 탐색하면 노드 연결이 길어질 수록 탐색 속도도 그 만큼 늘어나기 때문에 최악의 경우 시간복잡도가 O(n)이 됨 → 리스트 대신 트리 사용해서 시간 복잡도를 줄일 수 있음.

### **2) Open Addressing**

해시 충돌이 일어나면 다른 버켓에 데이터를 삽입하는 방식 → 데이터의 주소값이 바뀐다.

아래와 같은 방법들이 있다.

1. 선형 탐색(Linear Probing): 해시충돌 시 다음 버켓, 혹은 몇 개를 건너뛰어 데이터를 삽입한다.
    
    ![선형 탐색과 Chaning 기법의 성능 비교](https://prod-files-secure.s3.us-west-2.amazonaws.com/0e258c4f-23fc-499c-809b-ffd6fc64b9de/0e6aec0a-1e8f-4881-abfc-05c8a448f85f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-02-05_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.58.53.png)
    
    선형 탐색과 Chaning 기법의 성능 비교
    
2. 제곱 탐색(Quadratic Probing): 해시충돌 시 제곱만큼 건너뛴 버켓에 데이터를 삽입(1,4,9,16..)
3. 이중 해시(Double Hashing): 해시충돌 시 다른 해시함수를 한 번 더 적용한 결과를 이용함.

특징

- 체이닝처럼 포인터가 필요없고, 지정한 메모리 외 추가적인 저장공간도 필요없다.
- 삽입,삭제시 오버헤드가 적다.
- 저장할 데이터가 적을 때 더 유리하다.
    
    **→ Chaining에 비해 성능이 더 좋다.**