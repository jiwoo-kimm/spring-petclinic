# Spring Boot를 활용한 동물병원 웹 어플리케이션
* 소스 : https://github.com/SpringSource/spring-petclinic
* 강의 : https://www.inflearn.com/course/spring_revised_edition/dashboard


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
