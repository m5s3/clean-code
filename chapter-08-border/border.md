# 경계

## 목차

- 외부코드 사용하기
- 경계 살피고 익히기
- log4j 익히기
- 학습 테스트는 공짜 이상이다
- 아직 존재하지 않는 코드를 사용하기
- 깨끗한 경계

### intro

소프트웨어 경계를 깔끔하게 처리하는 기법과 기교를 살펴본다.

### 외부 코드 사용하기

인터페이스 제공자와 인터페이스 사용자 사이에는 특유의 긴장이 존재한다.
제공자는 적용성을 최대한 넓히려 애쓴다. 반면, 사용자는 자신의 요구에 집중하는 인터페이스를 바란다.

```java
public class Sensors {
    private Map sensors = new HashMap();

    public Sensor getById(String id) {
        return (Sensor) sensors.get(id);
    }
}
```

경계 인터페이스인 `Map` 을 `Sensors` 안으로 숨긴다. 따라서 `Map` 인터페이스가 변하더라도 나머지 프로그램에는 옇야을 미치지 않는다.
경계 인터페이스를 여기저기 넘기지 마라.
경계 인터페이스를 이용할 때는 이를 이용하는 클래스나 클래스 계열 밖으로 노출되지 않도록 주의해라.
경계 인터페이스를 공개 API의 인수로 넘기거나 반환값으로 사용하지마라.

### 경계 살피고 익히기

우리쪽 코드를 작성해 외부 코드를 호출하는 대신 먼저 간단한 테스트 케이스를 작성해서 외부 코드를 익히는 것을 **학습 테스트**라고 부른다.
학습 테스트는 프로그램에서 사용하려는 방식대로 외부 API를 호출한다. 즉, 통제된 환경에서 API를 제대로 이해하는지를 확인하는 것이다.
학습 테스트는 API를 사용하려는 목적에 초점을 맞춘다.

### log4j 익히기

```java
public class LogTest {
    private Logger logger;

    @Before
    public void initialize() {
        logger = Logger.getLogger("logger");
        logger.removeAllAppenders();
        Logger.getRootLogger().removeAllAppenders();
    }

    @Test
    public void basicLogger() {
        BasicConfigurator.configure();
        logger.info("basicLogger")
    }

    @Test
    public void addAppenderWithStream() {
        logger.addAppender(new ConsoleAppender(
            new PatternLayout("%p %t %m%n"),
            ConsoleAppender.SYSTEM_OUT));
        logger.info("addAppendWithStream")
    }

    @Test
    public void addAppenderWithoutStream() {
        logger.addAppender(new ConsoleAppender(
            new PatternLayout("%p %t %m%n"));
        logger.info("addAppendWithoutStream")
    }
}
```

모든 지식을 독자적인 로거 클래스로 캡슐화한다.
그러면 나머지 프로그램은 log4j 경계 인터페이스를 몰라도 된다.

### 학습 테스트는 공짜 이상이다

학습 테스트에 드는 비용은 없다.
오히려 필요한 지식만 확보하는 손쉬운 방법이다.
학습 테스트는 이해도를 높여주는 정확한 실험이다.
새 버전이 나와도 우리 코드와 호환되지 않으면 학습 테스트가 이 사실을 곧바로 밝혀낸다.
경계 테스트가 있다면 패키지의 새 버전으로 이전하기 쉬워진다.

### 아직 존재하지 않는 코드를 사용하기

경계와 관련해 또 다른 유형은 아는 코드와 모르는 코드를 분리하는 경계이다.
우리가 바라는 인터페이스를 구현하면 우리가 인터페이스를 전적으로 통제한다는 장점이 있다.
또한, 코드 가독성도 높아지고 코드 의도도 분명해진다.
이와 같은 설계는 테스트도 아주 편하다.

### 깨끗한 경계

소프트웨어 설계가 우수하다면 변경하는데 많은 투자와 재작업이 필요하지 않다.
통제하지 못하는 코드를 사용할 떄는 너무 많은 투자를 하거나 향후 변경 비용이 지나치게 커지지 않도록 각별히 주의해야 한다.
경계에 위치하는 코드는 깔끔히 분리한다.
또한, 기대치를 정의하는 테스트 케이스도 작성한다.
통제가 불가능한 외부 패키지에 의존하는 대신 통제가 가능한 우리 코드에 의존해라.
외부 패키지를 호출하는 코드를 가능한 줄여 경계를 관리하자.
새로운 클래스로 감싸거나 아니면 ADAPTER 패턴을 사용해 우리가 원하는 인터페이스를 패키지가 제공하는 인터페이스로 변환해라.
