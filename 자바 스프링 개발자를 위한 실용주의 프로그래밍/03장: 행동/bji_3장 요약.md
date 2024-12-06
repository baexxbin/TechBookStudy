### 3장 행동

#### 데이터 위주의 사고와 행동 위주의 사고

자동차를 만들어 달라는 요청에 두 개발자가 아래와 같이 구현함.

- A 개발자

```java filename="" copy showLineNumbers
public class Car {
  private Frame frame;
  private Engine engine;
  private Tire tire;
  ...
}
```

- B 개발자

```java filename="" copy showLineNumbers
public class Car {
  public void drive() {}
  public void changeDirection() {}
  public void accelerate() {}
  ...
}
```

A 개발자를 데이터 위주의 사고를 가진 개발자, B 개발자를 행동 위주의 사고를 가진 개발자라고 함. <br></br>

- 데이터 위주로 만들어진 클래스는 구조적인 데이터 덩어리를 만드는 데 사용하는 구조체와 다를바 없음.
  - 전혀 객체지향 스럽지 않음.
- 객체를 구분 짓는 요인은 데이터가 아닌 행동임.

#### 덕 타이핑이란

> 덕 테스트: 만약 어떤 새가 뒤뚱뒤뚱 걷고, 헤엄치고, 꽥꽥거리는 소리를 낸다면 나는 그 새를 오리라고 부를 것이다.

- 덕 타이핑은 덕 테스트에서 유래한 용어임.
- 위 말을 개발자 관점에서 보면 `행동이 같다면 같은 클래스로 부르겠다.`라는 의미.
- Typescript는 덕타이핑을 지원.

```ts filename="" showLineNumbers copy
class Duck {
  walk() {
    console.log('walk');
  }
  swim() {
    console.log('swim');
  }
}

class Person {
  walk() {
    console.log('walk');
  }
  swim() {
    console.log('swim');
  }
}

val duck: Duck = new Person();
```

- 행동이 곧 역할을 정의하고 역할이 곧 객체를 정의함.

#### 구현을 생각하면 데이터 위주의 사고가 된다

```java filename="" copy showLineNumbers
public class Car {
  private int degree; // 자동차의 각도(0도 ~ 360도)

  public void changeDirection(int degree) {
    this.degree = degree;
  }
}
```

- 방향을 바꾸는 행동을 구현할려고 하다보니 degree라는 필드가 생김.
  - 데이터 위주의 사고로 돌아옴.
  - 구현을 고민했기 때문.
- 행동을 고민하면서 구현이나 알고리즘을 고민해서는 안됨.
- 협업시 인터페이스를 정의해놓고 각자 자리에서 본인의 역할을 다하면 됨.

#### 인터페이스와 행동을 다르다

- 인터페이스는 외부에서 어떤 객체에게 행동을 시키고자 할 때 메시지를 보낼 수 있는 창구.
- 인터페이스란 어떤 행동을 지시하는 방법의 집합.

#### 행동 위주의 사고를 하는 방법

- 실체에 집중할 때 데이터 위주의 사고를 하고 역할에 집중할 때 행동 위주의 사고를 함.
  - ex : 자동차와 탈것, 자동차 -> 실체 / 탈것 -> 역할
- 행동과 역할에 집중하라는 것이 단순히 추상화를 많이 하라는 뜻이 아님.

#### 함수와 메서드의 차이

- 함수의 각 입력값은 정확히 하나의 출력값으로 대응됨.
  - 같은 입력에 대해 항상 같은 출력을 해야함.
  - 같은 입력에 대해 두 개의 출력을 갖는 것은 함수가 아님.
  - 예를 들어 Vehicle 인터페이스의 구현체 Car와 Airplane이 있을 때 vehicle.move() 함수의 결과가 다를 수 있다면 그건 함수가 아님.
- 메서드란 어떤 메시지를 처리해 달라는 요청을 받았을 때 이를 어떻게 처리하는지 방법(method)를 정의한 것.
