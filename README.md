# Spring Boot를 활용한 동물병원 웹 어플리케이션
* 소스 : [Spring 공식 예제 中 spring-petclinic](https://github.com/SpringSource/spring-petclinic)
* 강의 : [예제로 배우는 스프링 (개정판)](https://www.inflearn.com/course/spring_revised_edition/dashboard)


## Section 1 : PetClinic Setup (7/1)

### 개발환경

* Windows 10
* jdk 13.0.2
* Git
* Eclipse with m2e plugin
  * `Help -> Check for Updates` 에 m2e plugin이 있다면 설치 된 것
  * 없다면 `Help -> Install New Software` 에서 `m2e plugin - http://download.eclipse.org/technology/m2e/releases` 설치

### 실행방법

1) 저장소를 zip으로 다운 OR `git clone https://github.com/SpringSource/spring-petclinic.git`
2) 해당 폴더를 workspace로 Eclipse 실행
3) workspace에서 Git Bash Shell 열고 `./mvnw generate-sources` 입력하여 Maven Build
    - `Formatting violations found in the following files` 에러 발생 시 Git Bash Shell에 `./mvnw spring-javaformat:apply` 입력
4) Run Configuration on `PetClinicApplication.java`
5) 웹 브라우저 상에서 [http://localhost:8080] 접속

### 과제 1

1) FirstName 검색
   - view : FirstName 입력받기
   - controller : findByFirstName() 메소드 & sql문 추가

2) 검색어 포함 Name 검색
   - controller : sql문 조건 변경

3) Owner에 Age 필드 추가
   - view : 입력받고 출력하는 필드 각각 추가
   - controller : Owner 스키마에 Age 추가 & sql INSERT문에 Age 필드 추가
