### 1장 절차지향과 비교하기

- 순차지향과 절차지향은 엄밀히 다른 개념임.

  - 순차지향 프로그래밍 : 말 그대로 코드를 위에서 아래로 읽음.
  - 절차지향 프로그래밍 : **함수** 지향 프로그래밍.

- 절차지향은 책임을 **프로시저로 나누고 프로시저에 할당**.
- 객체지향은 책임을 **객체로 나누고 객체에 할당**.

#### C언어는 객체지향을 구현할 수 없는 이유

객체를 추상화한 역할에 책임을 할당함. 예를 들어서

```java filename="" copy showLineNumbers
public interface Calcuable {
  void calc(int a, int b)
}
```

이런식으로 인터페이스를 만들어서 객체를 추상화하고, 이 인터페이스를 구현한 클래스를 만들어서 책임을 할당함.<br></br>
그러나 C언어는 이런 추상화를 할 수 없으며, **추상화가 불가능하다는 특징 때문에 객체지향을 구현할 수 없음**.

#### 객체지향이란?

객체가 책임을 갖게 됐고 객체의 역할이 정해졌으며, **어떤 목표를 달성하기 위해서 서로 다른 객체와 협력을 함**. 이게 객체지향의 본질임.

#### 객체지향 사고방식, TDA

- Tell Dont Ask : 객체에게 물어보지 말고 시켜라 라는 원칙

예를 들어서, 아래와 같은 코드가 있다고 치면

```java filename="" copy showLineNumbers
public class Shop {
  public void sell(Account account, Product product) {
    if (account.getBalance() > product.getPrice()) {
      ...
    }
  }
}
```

이 코드는 객체에게 물어보는 코드임. 객체에게 물어보는 것이 아니라 객체에게 시키는 코드로 바꾸면 아래와 같음.

```java filename="" copy showLineNumbers
public class Shop {
  public void sell(Account account, Product product) {
    if(account.canBuy(product)) {
      ...
    }
  }
}
```

이러한 변경을 통해 아래와 같은 3가지 이점을 얻을 수 있음.

- 유연성 증가 : 각 객체가 자신의 상태와 동작을 관리하므로 외부에서 객체 내부의 상태를 직접 알 필요가 없음
- 결합도 감소 : 객체 내부의 세부 사항이 감춰지므로 다른 객체와의 상호 의존성을 줄일 수 있음.
- 재사용성 향상 : canBuy() 메서드를 다른 클래스에서도 사용할 수 있음.
