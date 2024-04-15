# 1장 스프링 부트 시작하기

## 1.1. 스프링 부트란

- 스프링 부트(Spring Boot)
    - 자바 웹 프로그램을 쉽고 편리하게 만들기 위한 도구
    - 스프링 프레임워크(Spring Framework)를 개선한 것
        - 대표적인 개선사항
            - 개발 환경 설정 간소화
            - 웹 애플리케이션 서버(WAS) 내장
    
    → 개발자가 개발에만 더 집중할 수 있음.
    

## 1.2. 스프링 부트 개발 환경 설정하기

개발 환경 설정 과정
: JDK 설치 → IDE 설치 → 스프링 부트 프로젝트 생성

### 1.2.1. JDK 설치하기

아래 사이트 접속

[Latest Releases | Adoptium](https://adoptium.net/temurin/releases/?os=windows&arch=x64&package=jdk&version=17)

운영체제 Windows / 아키텍처 x64 / 패키지 타입 JDK / 버전 17 - LTS 선택 후 .msi 다운로드

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/ba48a30a-1cc0-4ca6-8218-de9849cb11a6)

설치 파일 실행하여 Finish 버튼이 나올 때 까지 설치 진행

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/342c2439-c795-4b84-9189-f95e34fc85ca)

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/5bbfe513-7036-48a9-a282-565b9ca2fc9d)

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/c3a73831-79b1-43af-bc7a-9cfe22ff851a)

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/9e3f5fd9-2739-4438-8203-5af82ce3d427)

CMD 창에서 설치 확인

- java -version

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/189fd2e6-f392-4316-a54f-7798ce21d777)

### 1.2.2. IDE 설치하기

인텔리제이 다운로드

[최고의 Java 및 Kotlin IDE인 IntelliJ IDEA를 다운로드하세요](https://www.jetbrains.com/ko-kr/idea/download/?section=windows)

### 1.2.3. 스프링 부트 프로젝트 만들기

스프링 부트 프로젝트 만들고 “헬로 월드!” 출력하기

- 프로젝트 만들고 실행하기
    - 아래 사이트 접속
        
        [](https://start.spring.io/)
        
    - 프로젝트 세부 항목 설정
    - Project: Gradle - Groovy
    - Language: Java
    - Spring Boot: 3.2.4 (기본값 선택)
    - Packaging: Jar
    - Java: 17
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/f5c4974f-0109-4545-b64e-c6806654d901)
        
    - Artifact 수정
    : firstproject
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/b455c4ea-5b2b-42ce-bc2c-e919c5f569de)
        
    - 스프링 웹 도구 추가
        - Spring Web
        - H2 Database
        - Mustache
        - Spring Data JPA
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/1d852ba1-436c-42ed-997b-8a5ae3815082)
        
    - 프로젝트 내려받기
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/860e5f3c-b912-4084-ac6d-03704e98f9f8)
        
    - 다운로드 파일 확인
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/c4a7905c-bbe9-4a87-b309-402a66d43583)
        
    - 프로젝트 오픈
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/8ffbfa61-32e0-44a8-9539-f0431f0ef62c)
        
    - BUILD SUCCESS
    build: 소스 코드를 실행할 수 있는 독립적인 형태로 만드는 것.
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/c06119c3-6f23-4090-8005-e93868e1f06e)
        
    - 서버 동작 확인
    Started FirstprojectApplication….
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/7f03a26c-af15-49d7-99b2-698d7ec811dc)
        
    - 서버 접속하기
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/373ed8a8-60c7-40b1-a762-b6ce73cc88f2)
        
    - hello.html 생성
        
        ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <title>Title</title>
        </head>
        <body>
            <h1>헬로 월드!</h1>
        </body>
        </html>
        ```
        
    - 서버 재접속
    [http://localhost:8080/hello.html](http://localhost:8080/hello.html)
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/9d84d608-2e8e-47e2-9616-526f5febf1ce)
        
    
    ## 1.3. 웹 서비스의 동작 원리 이해하기
    
    웹 서비스는 클라이언트의 요청에 따른 서버의 응답으로 동작한다.
    
    ### 1.3.1. 클라이언트-서버 구조
    
    - **클라이언트**: 서비스를 사용하는 프로그램 or 컴퓨터
    ex) 웹 브라우저
    - **서버**: 서비스를 제공하는 프로그램 or 컴퓨터
    ex) 스프링 부트
    
    서버를 실행해야만 웹 브라우저를 통해 응답을 받을 수 있다.
    
    ### 1.3.2. http<h>://localhost:8080/hello.html의 의미
    
    - localhost
    내 컴퓨터의 주소인 127.0.0.1
    - 8080
    포트 번호를 의미함.
    - hello.html
    서버에 요청하는 파일을 의미함.
    cf) 스프링 부트의 경우 파일을 직접 지정할 경우
     src\main\resources\static 디렉터리에서 파일을 찾음.
    
    ⇒ 내 컴퓨터의 8080번의 서버에 hello.html 파일을 요청한다.
