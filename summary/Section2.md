# Section 2 : Spring IOC (7/2)

## MySQL 연동
#### 1) MySQL 8.0 Local에 설치
#### 2) MySQL, Eclipse 연동
  * Eclipse `Window - Show View - Other - Data Source Explorer`
  * `New Connection Profile`에 [`mysql-connector-java-5.1.49.jar`](https://dev.mysql.com/downloads/file/?id=496255) MySQL 등록
#### 3) timezone 설정
  * mysql 스키마에서 [Timezone : Non POSIX with leap seconds](https://downloads.mysql.com/general/timezone_2020a_leaps_sql.zip) 실행
  * `my.ini`에 `default-time-zone=Asia/Seoul` 추가
#### 4) application.properties 업데이트
```java
spring.datasource.url=${MYSQL_URL:jdbc:mysql://localhost:3306/petclinic}
spring.datasource.username=${MYSQL_USER:root}
spring.datasource.password=${MYSQL_PASS:myPassword}
spring.profiles.active=mysql
```

## Inversion of Control

### Dependency Injection
#### : 클래스에서 사용할 객체를 그 안에서 직접 만드는 대신, 클래스 외부에서 받아 옴
* `@Autowired`, `@Inject` annotation을 3가지 방법으로 붙여 의존성 주입 가능
##### 1) 생성자 : 단일 생성자 parameter에 객체를 받아 오도록 함
###### Spring 4.3 이상 : annotation 생략해도 자동으로 의존성 주입
```java
private final SampleRepository samples;

public SampleController(SampleRepository sampleRepository) {
  this.samples = sampleRepository;
}
```
##### 2) 필드
```java
@Autowired
private SampleRespository samples;
```
##### 3) Setter
```java
private SampleRespository samples;

@Autowired
public void setSamples(SampleRepository samples) {
  this.samples = samples;
}
```


### Bean
#### : IoC Container가 관리하는 객체
##### 1) Component Scanning<br>
 : `@Component`, `@Repository`, `@Controller`, `@Configuration`, `@Service` 등의 annotation이 붙은 모든 클래스의 객체가 Bean으로 등록됨
##### 2) Java Configuration<br>
 : `@Configuration`이 붙은 클래스 내 메소드에 `@Bean`을 붙이면 리턴 객체가 Bean으로 등록됨


### IoC Container
#### : Bean을 만들고 관리함
* ApplicationContext (BeanFactory 상속)
* IoC Container 내부의 Bean끼리의 의존성 주입만 할 수 있음
* ApplicationContext 객체를 통해 직접 Bean을 꺼낼 수 있음 (but 자동으로 해주기 때문에 쓸 필요 없음)
  ```java
  ApplicationContext applicationContext = new ApplicationContext();
  SampleClass bean = applicationContext.getBean(SampleClass.class);
  ```
