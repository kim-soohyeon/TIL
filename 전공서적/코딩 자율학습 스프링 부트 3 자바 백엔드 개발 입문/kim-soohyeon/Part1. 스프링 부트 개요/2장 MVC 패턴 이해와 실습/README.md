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
    

### 2.2.3. 모델 추가하기

1. 뷰 템플릿 페이지에 변수 삽입하기
- 머스테치 문법을 사용하여 변수를 추가한다.
- {{변수명}}
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/f4475daa-7379-42bd-bc78-b73447eb80dd)
    
2. 컨트롤러에 모델 추가하여 변수 등록하기
FirstController.java 파일을 수정하여 Model 타입의 model 매개변수를 추가한다.
    
    ```java
    package com.example.firstproject.controller;
    
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class FirstController {
    
        @GetMapping("/hi")
        public String niceToMeetYou(Model model){ // model 객체 받아오기
            model.addAttribute("username", "수현");
            return "greetings"; //greetings.mustache 파일 반환
        }
    }
    
    ```
    
3. 서버 재기동 후 확인
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/bef755ba-f524-4f86-a403-7902c49ff8cb)
    

### * 핵심정리

- 뷰 템플릿: 웹 페이지를 일종의 틀로 만든 것.
- 컨트롤러: 클라이언트의 요청을 받아 서버에서 이를 처리하는 역할
- 모델: 뷰 템플릿에서 사용되는 데이터를 관리하는 역할
- @Controller: 이 클래스가 컨트롤러임을 선언함.
- @GetMapping: 클라이언트가 URL 요청을 받아 특정 컨트롤러의 메서드가 처리하게 함.

## 2.3. MVC의 역할과 실행 흐름 이해하기

### 2.3.1. /hi 페이지의 실행 흐름

### 2.3.2. /bye 페이지의 실행 흐름

- seeYouNext 메서드 작성
    
    ```java
    @GetMapping("/bye")
    public String seeYouNext(Model model){ // model 객체 받아오기
        model.addAttribute("username", "수현");
        return "goodbye"; //goodbye.mustache 파일 반환
    }
    ```
    
- goodbye.mustache 파일 생성
    
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
        <h1>{{username}}님, 다음에 또 만나요!</h1>
    </body>
    </html>
    ```
    
- 결과 확인
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/605aacaf-8474-4844-a34f-2d4d74495b05)
    

## 2.4. 뷰 템플릿 페이지에 레이아웃 적용하기

- 레이아웃(layout): 화면에 요소를 배치하는 일
- 헤더-푸터 레이아웃(header-footer layout): 가장 기존이 되는 레이아웃. 샌드위치 구조.
    - 헤더(header) 영역에는 내비게이션 삽입
    - 푸터(footer) 영역에는 사이트 정보 삽입
    - 헤더와 푸터 사이 영역에는 콘텐트(content)를 배치함.

### 2.4.1. /hi 페이지에 헤더-푸터 레이아웃 적용하기

부트스트랩을 활용하여 페이지를 쉽고 빠르게 꾸민다.

cf) 부트스트랩(Bootstrap): 웹 페이지를 쉽게 만들 수 있도록 작성해 놓은 코드 모음

1. 부트스트랩 홈페이지 접속
v5.0.2
    
    [Introduction](https://getbootstrap.com/docs/5.0/getting-started/introduction/#starter-template)
    
2. 스타터 템플릿 코드 복사
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/7cb95c5b-85d6-4734-8dfb-ab91edc16470)
    
3. greetings.mustache 파일에 적용
    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
    
        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    
        <title>Hello, world!</title>
    </head>
    <body>
        <!--navigation-->
    
        <!--content-->
        <h1>{{username}}님, 다음에 또 만나요!</h1>
    
        <!--site info-->
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
    </html>
    ```
    
4. navbar 검색 후 코드 복사
    
    [Navbar](https://getbootstrap.com/docs/5.0/components/navbar/)
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/2d1665c1-0c75-4e4c-bc66-008cab9d8e35)
    
5. 내비게이션 소스 적용
    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
    
        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    
        <title>Hello, world!</title>
    </head>
    <body>
        <!--navigation-->
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">Navbar</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Home</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#">Link</a>
                        </li>
                        <li class="nav-item dropdown">
                            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                                Dropdown
                            </a>
                            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                                <li><a class="dropdown-item" href="#">Action</a></li>
                                <li><a class="dropdown-item" href="#">Another action</a></li>
                                <li><hr class="dropdown-divider"></li>
                                <li><a class="dropdown-item" href="#">Something else here</a></li>
                            </ul>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
                        </li>
                    </ul>
                    <form class="d-flex">
                        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                        <button class="btn btn-outline-success" type="submit">Search</button>
                    </form>
                </div>
            </div>
        </nav>
    
        <!--content-->
        <h1>{{username}}님, 다음에 또 만나요!</h1>
    
        <!--site info-->
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
    </html>
    ```
    
6. 내비게이션 바 확인
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/ce6560d2-2959-4699-a2c3-6b484561e4c2)
    
7. 푸터 추가 및 콘텐트 스타일 변경
    
    ```html
    <!doctype html>
    <html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
    
        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    
        <title>Hello, world!</title>
    </head>
    <body>
        <!--navigation-->
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">Navbar</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Home</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#">Link</a>
                        </li>
                        <li class="nav-item dropdown">
                            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                                Dropdown
                            </a>
                            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                                <li><a class="dropdown-item" href="#">Action</a></li>
                                <li><a class="dropdown-item" href="#">Another action</a></li>
                                <li><hr class="dropdown-divider"></li>
                                <li><a class="dropdown-item" href="#">Something else here</a></li>
                            </ul>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
                        </li>
                    </ul>
                    <form class="d-flex">
                        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                        <button class="btn btn-outline-success" type="submit">Search</button>
                    </form>
                </div>
            </div>
        </nav>
    
        <!--content-->
        <div class="bg-dark text-white p-5">
            <h1>{{username}}님, 반갑습니다!</h1>
        </div>
    
        <!--site info-->
        <div class="mb-5 container-fluid">
            <hr>
            <p>ⓒ CloudStudying | <a href="#">Privacy</a> | <a href="#">Terms</a></p>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
    </html>
    ```
    
8. 푸터 및 콘텐트 적용 확인
    
    ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/fc166c73-1f83-4e35-9d43-279ed22dbd06)
