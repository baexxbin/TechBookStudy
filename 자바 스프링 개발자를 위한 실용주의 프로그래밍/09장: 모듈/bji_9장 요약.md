### 9장 모듈

#### 모듈이란

- 어떤 목적을 수행하기 위해 분리된 작은 구성 단위를 뜻함.
- 소프트웨어 공학에서 말하는 모듈이란 프로그램의 기본 구성요소이면서 라이브러리를 포괄하는 조금 더 큰 규모의 용어임.
- **독립성**과 **은닉성**을 만족하며 연관된 코드들의 묶음.
- 따라서 모듈 시스템이란 **의존성 관리**와 **캡슐화 관리**에 대한 정보를 제공할 수 있어야 함.
  - 의존성 관리 : 모듈을 사용하기 위해 어떤 의존성이 필요한지 명시할 수 있어야 함.
  - 캡슐화 관리 : 모듈은 불필요한 구현을 외부로 드러내지 않아야 함.

#### Angular or NestJS or JS의 모듈

- import를 통해 의존성을 명시해주고 export를 통해 사용가능한 인터페이스를 제공함.

##### java 모듈 디스크립터

- java 9에서 module-info.java라는 모듈 디스크립터를 도입.
- module-info.java라는 파일을 통해서 모듈 시스템을 구현.
- 그럼 java 9 이전에는 모듈의 개념이 없었냐? 👉 맞음.

#### 독립성

- 모듈이 독립적이어야 하는 이유는 유지보수를 용이하게 하고, 확장성을 높이고, 코드의 재사용성을 높이기 위함.
- 코드를 테스트하기 쉽게 만들 수 있어 전체 시스템의 품질을 높이는데 기여.
- A라는 패키지가 B 패키지에 의존하면 A 패키지의 독립성이 상대적으로 떨어질 수 있음.
  - 👉 단 절대적으로 A 패키지가 "독립성이 떨어진다."라고 표현할 수는 없음.
- 모듈이 독립적이기 위해선 다음과 같은 룰들을 지켜야 함.
  - 최대한 내부에서 해결하라.
  - 외부에는 강하게 의존하지 마라.
  - 외부 시스템을 사용한다면 외부 시스템의 사용을 명시하라.

##### 하위 의존성 추적 기능으로 얻을 수 있는 이점

- 하위 모듈의 중복 검사와 불필요한 의존성이 있는지 검사할 수 있음.
- 하위 모듈에 보안 취약점이 생겼을 때 상위모듈 파악하기 쉬워짐.
- 동적 로딩이 가능해짐.
  - 자바 스크립트에는 **트리 셰이킹(tree shaking)**이라는 개념이 있음.
  - 애플리케이션에서 사용되지 않는 코드를 식별해 제거함으로써 번들(bundle) 파일의 크기를 줄이고 성능을 향상 시킴.

#### 은닉성

- 하이럼 법칙

> API 사용자가 충분히 많다면 계약을 어떻게 했는지는 크게 중요하지 않습니다.
> 시스템의 모든 관측 가능한 행동은 사용자에 의해 결정될 것입니다.

- API를 온갖 해괴망측한 방법으로 사용함.
- API에 할당된 암묵적 책임을 기대하고 사용하는 사용자가 많아질 수 있음.
- 자바 패키지 시스템이 문제임.

> 예를 들어, 어떤 라이브러리에 TEMP라는 의존성이 있었는데 A 개발자가 TMEP의 의존성을 더 이상 사용하지 않고 메이저 버전을 올렸음.
> 그런데 해당 라이브러리를 사용하는 B 개발자가 TEMP에 있는 코드를 사용하는 상황이 생김.
> B 개발자가 A 개발자에게 롤백을 요청하는 경우 발생.
> 이처럼, 사용자 뿐만이 아닌 라이브러리 개발자라면 개발자 역시 내 라이브러리를 온갖 해괴망측한 방법으로 사용할 수 있다는 사실을 고려해야 함.

- 몽키 패치

> 파이썬에서 프로그램이 실행되는 런타임에 동적으로 코드를 수정해서 기존 클래스나 모듈, 함수 등의 동작을 변경하는 것을 말함.
> 외부 라이브러리에 있는 버그를 임시로 수정하는데 유용하지만 개발자들이 온갖 해괴망측한 방법으로 사용.

#### 패키지 구조

##### 계층 기반 구조

```bash filename="" copy
project
└── src/main/java
    └── com.demo.myapp
        ├── presentation
        │   ├── UserController.java
        │   ├── CafeController.java
        │   ├── BoardController.java
        │   └── PostController.java
        ├── business
        │   ├── UserService.java
        │   ├── CafeService.java
        │   ├── BoardService.java
        │   ├── PostService.java
        │   └── repository
        │       ├── UserRepository.java
        │       ├── CafeRepository.java
        │       ├── BoardRepository.java
        │       └── PostRepository.java
        ├── domain
        │   ├── User.java
        │   ├── Cafe.java
        │   ├── Board.java
        │   └── Post.java
        └── infrastructure
            ├── UserRepositoryImpl.java
            ├── UserJpaEntity.java
            ├── UserJpaRepository.java
            ├── CafeRepositoryImpl.java
            ├── CafeJpaEntity.java
            ├── CafeJpaRepository.java
            ├── BoardRepositoryImpl.java
            ├── BoardJpaEntity.java
            ├── BoardJpaRepository.java
            ├── PostRepositoryImpl.java
            ├── PostJpaEntity.java
            └── PostJpaRepository.java
```

- 레이어에 관한 약간의 이해와 이에 대응하는 스프링 컴포넌트가 무엇인지만 알면 누구나 쉽게 개발할 수 있음.
- 도메인이 눈에 들어오지 않는다는 단점이 있음.
- 비즈니스 코드를 한곳에 모아 볼 수 없음.

##### 도메인 기반 구조

```bash filename="" copy
project
└── src/main/java
    └── com.demo.myapp
        ├── user
        │   ├── presentation
        │   │   └── UserController.java
        │   ├── application
        │   │   └── UserService.java
        │   ├── repository
        │   │   └── UserRepository.java
        │   ├── domain
        │   │   └── User.java
        │   └── infrastructure
        │       ├── UserRepositoryImpl.java
        │       ├── UserJpaEntity.java
        │       └── UserJpaRepository.java
        ├── cafe
        │   ├── presentation
        │   │   └── CafeController.java
        │   ├── application
        │   │   └── CafeService.java
        │   ├── repository
        │   │   └── CafeRepository.java
        │   ├── domain
        │   │   └── Cafe.java
        │   └── infrastructure
        │       ├── CafeRepositoryImpl.java
        │       ├── CafeJpaEntity.java
        │       └── CafeJpaRepository.java
        ├── board
        │   ├── presentation
        │   │   └── BoardController.java
        │   ├── application
        │   │   └── BoardService.java
        │   ├── repository
        │   │   └── BoardRepository.java
        │   ├── domain
```

- 계층 기반 구조보다는 복잡해짐.
- 도메인이 눈에 들어옴.
