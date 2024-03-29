## OOP - 객체지향 프로그래밍

필요한 데이터를 추상화 하여 속성과 행위를 가진 객체를 만들고 그 객체들 간의 상호작용으로 로직을 구성하는 프로그래밍 기법

→ 데이터와 함수를 객체로 관리한다! - 일방적으로 사용하는 언어 구조

## OOP의 4가지 특징

- 캡슐화
    
    → **객체**의 **속성**과 **행위**를 **하나**로 묶어 코드를 외부에 감춰 은닉한다.
    
    데이터와 처리 행위를 묶고 외부에는 보여지지 않는다.
    
    객체 모듈화 지향 & 모듈 단위 코드 재사용 → 코드 유지보수 이점
    
- 추상화
    
    → 중요하고 필요한 정보만을 표현하기 위해서, 객체의 공통적인 속성과 행위를 하나로 묶는다.
    
- 상속
    
    → 상위 클래스에서 정의된 기능을 가져와 재사용하거나 새로운 기능을 추가한다.
    
    코드의 중복을 줄이고 재사용성을 늘릴 수 있음
    
- 다형성
    
    → 객체가 상속을 통해 기능을 확장, 변경하여 여러 행태의 객체로 재구성한다.
    
    Overloading, Overriding을 통해 다형성 확인
    
    Overloading → 상위 클래스에 동일한 이름을 가진 함수가 있을 때, 하위 클래스에서 기능을 재정의
    
    Overriding → 하나의 클래스 안에 같은 이름을 가진 함수 여러개 → 인자들은 다름 
    

### **OOP의 장/단점**

---

> 장점
> 
- 높은 **코드 재사용**성 : 다형성이 있고, 캡슐화를 통해 모듈화가 가능하기 때문
- **생산성** 향상 : 캡슐화로 객체의 독립성이 높기 때문
- **자연적 모델링** 가능 : 일상의 언어와 유사하다는 장점이 있기 때문
- **유지 보수**의 **우수**성 : 캡슐화로 객체의 독립성이 높고, 다형성이 있어 기능 변경이 용이함

> 단점
> 
- **개발 속도**가 느림 : 모델링 과정에서 시간이 오래 걸리기 때문
- **절차 지향**에 **비해, 실행 속도**가 **느림** : 클래스를 확인 후, 실행되기 때문
- **객체**가 **많아짐**에 따라 **용량**이 커짐 : Instance의 증가로 인한 문제점