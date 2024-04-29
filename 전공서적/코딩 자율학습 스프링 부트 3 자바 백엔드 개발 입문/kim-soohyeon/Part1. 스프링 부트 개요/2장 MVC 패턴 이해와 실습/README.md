# 2장 MVC 패턴 이해와 실습

## 2.1. 뷰 템플릿과 MVC 패턴

### 2.1.1. 뷰 템플릿이란

- 뷰 템플릿(View Template)
    - 화면을 담당하는 기술
    - 웹 페이지(View)를 하나의 틀(Template)로 만들고 변수를 삽입해 서로 다른 페이지를 보여줌.
    - 뷰 템플릿 생성 도구 머스테치(Mustache)
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/faba1cb6-ac07-4912-a143-855d68f8780a)
        

### 2.1.2. MVC 패턴

- 컨트롤러(Controller)
    - 클라이언트의 요청을 받아 서버에서 처리하는 역할
- 모델(Model)
    - 데이터를 관리하는 역할
- 뷰(View)
    - 웹 페이지를 화면에 보여주는 역할
- MVC 패턴(Model-View-Controller Pattern)
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/99ed6ee4-5c96-43ac-a1d8-9a91a668d018)
	

## 2.2. MVC 패턴을 활용해 뷰 템플릿 페이지 만들기

### 2.2.1. 뷰 템플릿 페이지 만들기

src > main > resources > templates 디렉터리에 뷰 템플릿을 생성함.

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/713761a0-eb72-468e-b2f6-b9ad832f6688)

1. 뷰 템플릿 파일 만들기
src > main > resources > templates 디렉터리에서 New → File을 선택함.
greetings.mustache 파일 생성
cf) mustache: 뷰 템플릿을 만드는 도구. 뷰 템플릿 엔진
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/4458636b-33b7-4abc-b336-99b0e95aa9ac)
    
2. 머스테치 플러그인 설치
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/a060b4d4-9b4b-437d-be81-1b563979a172)
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/6cbf15aa-696c-4419-a7a9-6abcd38d4a50)
    
3. 뷰 템플릿 코드 작성
greetings.mustache 파일 제일 윗줄에 doc 입력 후 Tab 키 입력 → 기본 HTML 코드 작성됨.
<h1> 태그를 추가하여  뷰 템플릿 페이지를 작성한다.
    
    ```html
    <html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <h1>수현님, 반갑습니다!</h1>
    </body>
    </html>
    ```
    

### 2.2.2. 컨트롤러 만들고 실행하기

1. 컨트롤러 패키지 생성하기
    
    컨트롤러는 src > main > java 디렉터리의 기본 패키지인 com.example.firstproject 안에
    
    New → Package를 선택하여 controller 패키지를 생성한다.
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/04c97efa-1dc3-4677-bd4b-ba0673ac0183)
    
2. FirstController.java 생성
    
    New → Java Class 선택 후 FirstController 생성
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/08c4a0e7-5b16-4157-83cf-296a081d43b7)

3. FirstController 작성
@Controller 어노테이션 추가
cf) 어노테이션(annotation): 소스 코드에 추가해 사용하는 메타 데이터의 일종
    
    ```java
    package com.example.firstproject.controller;
    
    import org.springframework.stereotype.Controller;
    
    @Controller
    public class FirstController {
    
        public String niceToMeetYou(){
            return "";
        }
    }
    ```
    
4. greetings.mustache 파일 반환
localhost:8080/hi 로 접속 시 greetings.mustache 파일 반환
    
    ```java
    package com.example.firstproject.controller;
    
    import org.springframework.stereotype.Controller;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class FirstController {
    
        @GetMapping("/hi")
        public String niceToMeetYou(){
            return "greetings"; //greetings.mustache 파일 반환
        }
    }
    
    ```
    
5. 서버 실행하기
메인 메서드에서 실행하기(FirstprojectApplication.java)
6. 결과 확인
localhost:8080/hi 로 접속
6.1. 한글 깨짐 발생
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/d9495dd7-0360-47a5-9806-8f28b467ccdd)
    
    6.2. application.properties 수정 후 서버 재시작
    
    ```java
    server.servlet.encoding.force=true
    ```
    
    6.3. 서버 기동 성공
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/916e462e-e7db-4f17-8611-a61c80db14ef)
