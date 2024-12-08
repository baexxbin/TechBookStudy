### 11장 알아두면 유용한 스프링 활용법

- interface를 List로 Bean 주입을 받게 되면 해당 interface를 구현한 모든 Bean이 들어오게 됨.

```java filename="" copy showLineNumbers
public interface NotificationChannel {
  void notify();
  boolean supports(Account account);
}

public class NotificationService {
  private final List<NotificationChannel> notificationChannels;

  public void notify(Account account, String message) {
    if (notificationChannels.supports(account)) {
      NotificationChannel.notify(account, message);
    }
  }
}
```

- 자기호출.
  - 아래 코드는 Transactional이 적용이 안됨.

```java filename="" copy showLineNumbers
@Controller
@RequiredArgsConstructor
class MyClass {
  private final MyService myService;

  @GetMapping
  @ResponseStatus(OK)
  public Object doSomething() {
    myService.doSomething1();
    return null;
  }
}

@Service
@RequiredArgsConstructor
class MyService {
  public void doSomething1() {

  }

  @Transactional
  public void doSomething2() {

  }
}
```
