# Section 2 : Spring IOC (7/2)

## MySQL 연동
1) MySQL 8.0 Local에 설치
2) MySQL, Eclipse 연동
  * Eclipse `Window - Show View - Other - Data Source Explorer`
  * `New Connection Profile`에 [`mysql-connector-java-5.1.49.jar`](https://dev.mysql.com/downloads/file/?id=496255) MySQL 등록
3) timezone 설정
  * mysql 스키마에서 [Timezone : Non POSIX with leap seconds](https://downloads.mysql.com/general/timezone_2020a_leaps_sql.zip) 실행
  * `my.ini`에 `default-time-zone=Asia/Seoul` 추가
4) application.properties 업데이트
    ```
    spring.datasource.url=${MYSQL_URL:jdbc:mysql://localhost:3306/petclinic}
    spring.datasource.username=${MYSQL_USER:root}
    spring.datasource.password=${MYSQL_PASS:myPassword}
    spring.profiles.active=mysql
    ```
