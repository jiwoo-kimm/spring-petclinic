# Section 3 : Spring AOP (7/3)

## Aspect Oriented Programming
### 흩어져 있는 공통된 코드를 한 곳에 모아 모듈화하는 기법

### 구현 방법
#### 1) 컴파일
* `A.java` ----`AOP`----> `A.class`
* class 파일 자체에 중복된 코드를 모두 포함하여 컴파일
* AspectJ 컴파일러가 제공
#### 2) 바이트코드 조작
* `A.java` ---> `A.class` ---`AOP`---> 메모리
* class를 메모리에 로딩하는 시점에 중복된 코드를 조작
* AspectJ Class loader가 제공
#### 3) 프록시 패턴
* Spring AOP가 사용하는 방법
* 기존 코드와 별도로, 중복되는 코드를 별도의 클래스로 작성
* 기존 코드를 건드리지 않고 중복 코드를 작성하는 것이 포인트

### 프록시 패턴 구현
#### 1) Interface
```java
public interface Payment {
  void pay(int amount);
} 
```

#### 2) Sample Class
```java
public class Cash implements Payment {
  public void pay(int amount) {
    System.out.println("Cash : " + amount);   // 원래 실행할 메소드
  }
}
```

#### 3) SamplePerf Class
```java
public class CashPerf implements Payment {
  Payment cash = new Cash();
  
  public void pay(int amount) {
    StopWatch stopWatch = new StopWatch();  // 추가로 실행할 중복 메소드
    stopWatch.start();
    
    cash.pay(amount);   // 원래 메소드 호출
    
    stopWatch.stop();
    System.out.println(stopWatch.prettyPrint());
  }
}
```

#### 4) Test Class
```java
public class Store {
  Payment payment;
  
  public Store(Payment payment){
    this.payment = payment;
  }
  
  public void buySomething(int amount) {
    payment.pay(amount);
  }
}
```

```java
public class paymentTest {
  @Test
  public void testPay() {
    CashPerf cashPerf = new CashPerf();  // CashPerf 객체로 Cash 호출
    Store store = new Store(cashPerf);
    store.buySomething(100);
  }
}
```
* 참고링크 : [Refactoring GURU](https://refactoring.guru/design-patterns/proxy)

### Spring @AOP
#### 1) `@LogExecutionTime`
* 어디에 Proxy 적용할 지 표시하는 Annotation
```java
@Target(ElementType.METHOD)         // Method 대상 사용
@Retention(RetentionPolicy.RUNTIME) // 유지할 기간
public @interface LogExecutionTime {
}
```

#### 2) `LogAspect`
* `@LogExecutionTime` Annotation 위치에서 처리할 클래스
* `joinPoint` : `@LogExecutionTime`이 붙어 있는 메소드
```java
@Component
@Aspect
public class LogAspect {
  Logger logger = LoggerFactory.getLogger(LogAspect.class); // Sys.out 대신 로거로 출력
  
  @Around("@annotation(LogExecutionTime)")
  public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
    StopWatch stopWatch = new StopWatch();  // 추가로 실행할 중복 메소드
    stopWatch.start();
    
    Object proceed = joinPoint.proceed();   // 원래 joinPoint의 메소드 호출
    
    stopWatch.stop();
    logger.info(stopWatch.prettyPrint());
    
    return proceed; // 실행 결과 return
  }
}
```
