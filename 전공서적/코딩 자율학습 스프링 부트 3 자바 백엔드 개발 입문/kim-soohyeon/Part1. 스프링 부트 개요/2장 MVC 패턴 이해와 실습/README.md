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

![Untitled](2%E1%84%8C%E1%85%A1%E1%86%BC%20MVC%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%8B%E1%85%AA%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%203807564a51fd4df9bedb5b327d58fba0/Untitled%202.png)

1. 뷰 템플릿 파일 만들기
src > main > resources > templates 디렉터리에서 New → File을 선택함.
greetings.mustache 파일 생성
cf) mustache: 뷰 템플릿을 만드는 도구. 뷰 템플릿 엔진
    
    ![Untitled](2%E1%84%8C%E1%85%A1%E1%86%BC%20MVC%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%8B%E1%85%AA%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%203807564a51fd4df9bedb5b327d58fba0/Untitled%203.png)
    
2. 머스테치 플러그인 설치
    
    ![Untitled](2%E1%84%8C%E1%85%A1%E1%86%BC%20MVC%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%8B%E1%85%AA%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%203807564a51fd4df9bedb5b327d58fba0/Untitled%204.png)
    
    ![Untitled](2%E1%84%8C%E1%85%A1%E1%86%BC%20MVC%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%8B%E1%85%AA%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%203807564a51fd4df9bedb5b327d58fba0/Untitled%205.png)
    
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
    
    ![Untitled](2%E1%84%8C%E1%85%A1%E1%86%BC%20MVC%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%8B%E1%85%AA%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%203807564a51fd4df9bedb5b327d58fba0/Untitled%206.png)
    
2. FirstController.java 생성
    
    New → Java Class 선택 후 FirstController 생성
    
    ![Untitled](2%E1%84%8C%E1%85%A1%E1%86%BC%20MVC%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%20%E1%84%8B%E1%85%B5%E1%84%92%E1%85%A2%E1%84%8B%E1%85%AA%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%203807564a51fd4df9bedb5b327d58fba0/Untitled%207.png)