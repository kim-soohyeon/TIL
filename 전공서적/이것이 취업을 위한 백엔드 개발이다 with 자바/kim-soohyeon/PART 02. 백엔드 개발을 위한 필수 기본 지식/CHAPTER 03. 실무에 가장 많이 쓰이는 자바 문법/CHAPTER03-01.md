# CHPTER 03. 실무에 가장 많이 쓰이는 자바 문법

# 1. 실습 환경 구축하기

## IDE(Integrated Development Environment)

- 통합개발환경. 개발에 필요한 각종 작업을 도와주는 S/W
- 기능
    - 소스코드 편집기
        - 코드를 직접 작성하고 편집할 수 있는 기능
        - 올바른 코드인지 검사하는 기능
        - 자동완성 기능
    - 빌드 자동화
        - cf) 빌드: 소스코드를 컴퓨터가 실행가능한 바이너리 코드 형태로 변환하는 것. 테스트 기능까지 포함됨.
        - 빌드를 자동화해주는 것
    - 디버거
        - 소스코드의 문제점을 분석하는 프로그램
- 이클립스, 인텔리제이, 비주얼 스튜디오 코드 등

## 인텔리제이 설치

[최고의 Java 및 Kotlin IDE인 IntelliJ IDEA를 다운로드하세요](https://www.jetbrains.com/ko-kr/idea/download/?section=windows)

## 기본 프로젝트 생성

자바 프로젝트로 ‘Hello World!’ 문자열 출력하기

![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/2b09eb44-b564-41e0-a6ba-1e22cc9e3906)

- File > New > Project
    - [Language]: java
    - [Build System]: IntelliJ
    - [JDK]: 17
    **cf. JDK와 SDK**
    - **SDK(Software Development Kit)**
    : S/W를 개발하기 위해 필요한 도구의 모음
    - **JDK(Java Development Kit)**
    : SDK의 한 종류인 자바 애플리케이션 개발 도구
        - JDK Download
        [Vendor]의 Eclipse는 IDE가 아니라 JDK를 배포하는 재단의 이름. Eclipse 재단에서 배포하는 Temurin이라는 JDK 17 버전 다운로드
            - [Version]: 17
            - [Vendor]: Eclipse Temurin
            
            ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/28b73949-4fde-4626-b2bc-39fd912ac2ce)
            
    - **JDK(Java Development Kit)**
        
        ![Untitled](https://github.com/kim-soohyeon/TIL/assets/59382707/4daa20a5-79b7-4aaf-8c70-6040ae547cd1)
        
        - 자바 개발에 필요한 도구를 포함하는 S/W
        - 구성 요소
            - 자바 컴파일러
                - .java → .class로 컴파일
            - JRE(Java Runtiome Environment)
                - .class 파일을 실행할 수 있는 환경을 제공하는 S/W
            - JVM(Java Virtual Machine)
                - JRE의 일부로 .class 파일을 실행하는 주체
    - Open JDK
        - 오픈 소스로 공개된 JDK. 상업적 사용 가능
    - Oracle JDK
        - 기업에서 사용하려면 라이선스 사용료 지급 필요
    - LTS(Long Term Support)
        - 장기간 기술 지원을 받을 수 있다는 의미
        - JDK 8, 11, 17, 21 버전이 이에 해당됨