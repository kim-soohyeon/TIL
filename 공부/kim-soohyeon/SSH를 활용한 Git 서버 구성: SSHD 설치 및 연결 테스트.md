# SSH를 활용한 Git 서버 구성: SSHD 설치 및 연결 테스트 

이 포스팅에서는 Windows 환경에서 SSH를 활용해 Git 서버를 구성하는 방법을 다룹니다. 첫 번째 단계로, Git 설치 및 OpenSSH 서버 설치, 설정, 그리고 클라이언트 PC에서 SSH 연결 테스트를 진행합니다.

## 1. Git 설치 (서버 및 클라이언트 PC)

1. **Git 설치**: 서버와 클라이언트 PC에 Git을 설치합니다.
- 설치 파일: [Git-2.45.2-64-bit.exe](https://git-scm.com/download/win)
- 설치 후, `Git Bash`에서 사용자 이름과 이메일을 설정합니다.
    
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    ```
    

## 2. OpenSSH 서버 설정 (서버 PC)

Windows에서 OpenSSH 서버를 설치하여 SSH 접속을 설정합니다.

### 2.1. OpenSSH 설치

1. **Windows 설정**을 통해 OpenSSH 서버를 설치합니다:
    - **앱** > **선택적 기능** > **기능 추가**로 이동
    - **OpenSSH 서버**를 선택하여 설치
2. **PowerShell**을 통한 설치:
    - 위 방법이 동작하지 않으면, PowerShell에서 다음 명령어를 실행해 설치합니다.
        
        ```powershell
        Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
        ```
        

### 2.2. SSH 설정 확인 및 수정

1. **SSH 설정 파일 (`sshd_config`) 수정**:
    - 설정 파일 위치: `C:\ProgramData\ssh\sshd_config`
    - 다음 설정이 적용되었는지 확인합니다:
        
        ```bash
        PubkeyAuthentication yes
        AuthorizedKeysFile .ssh/authorized_keys
        PasswordAuthentication no
        ```
        

### 2.3. SSH 키 인증 설정

1. **클라이언트 PC에서 SSH 공개키 (`id_rsa.pub`) 생성**:
    - 생성된 공개키를 서버의 `authorized_keys` 파일에 추가합니다.
    
    ```bash
    cd ~/.ssh
    echo "복사한 공개 키 내용" >> ~/.ssh/authorized_keys
    chmod 600 ~/.ssh/authorized_keys
    chmod 700 ~/.ssh
    ```
    
    이제 클라이언트 PC에서 비밀번호 없이 SSH 키를 통해 서버에 접속할 수 있습니다.
    

### 2.4. `sshd` 서비스 시작 및 자동 실행 설정

1. **PowerShell**을 관리자 권한으로 실행하여 `sshd` 서비스를 시작하고 자동 실행을 설정합니다.
    
    ```powershell
    PS C:\Windows\system32> Start-Service sshd
    PS C:\Windows\system32> Get-Service sshd
    
    Status   Name               DisplayName
    ------   ----               -----------
    Running  sshd               OpenSSH SSH Server
    PS C:\Windows\system32> Set-Service -Name sshd -StartupType 'Automat
    ```
    

### 2.5. 방화벽 설정

1. **SSH 포트(기본 22번) 열기**:
    - PowerShell에서 다음 명령어를 실행하여 방화벽 규칙을 추가합니다.
        
        ```powershell
        New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 
        ```
        

## 3. SSH 클라이언트 설정 및 원격 저장소 설정 (클라이언트 PC)

1. **SSH 키 생성**
    - `Git Bash`에서 SSH 키를 생성합니다.
    
    ```bash
    ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
    ```
    
    - 생성된 `id_rsa.pub` 파일을 서버 PC의 `authorized_keys` 파일에 복사하여 추가합니다. (2.3 참고)
2. **서버 PC에 SSH 연결 테스트**
    - 다음 명령어로 서버에 SSH 접속을 시도합니다.
        
        ```bash
        ssh KimSoohyun@10.10.10.100
        ```
        
        명령어를 실행하면, SSH 클라이언트는 `10.10.10.100` IP 주소를 가진 서버에 접속을 시도합니다. 접속이 성공하면, `KimSoohyun` 계정으로 서버에 로그인하여 터미널을 통해 명령을 실행할 수 있는 상태가 됩니다.
        

## 4. Git 저장소 생성 (서버 PC)

- 서버 PC에서 `Git Bash`를 열고, 원격 저장소로 사용할 디렉토리를 만듭니다.
    
    ```bash
    mkdir -p /c/Users/soohyeon/repositories
    cd /c/Users/soohyeon/repositories
    git init --bare
    ```
    
- `-bare` 옵션은 이 저장소가 개발 작업이 아닌, 원격 저장소로만 사용된다는 것을 의미합니다.

## 5. 원격 저장소 추가 및 테스트 (클라이언트 PC)

1. **원격 저장소 추가**
    - 클라이언트 PC에서 다음 명령어를 실행하여 원격 저장소를 클론합니다.
        
        ```bash
        git clone ssh://your_username@server_ip/path/to/repository
        ```
        
2. 에러 발생
- 에러 로그
    
    ```bash
    chunjae@DESKTOP-0IMOPG5 MINGW64 ~/repo_client
    $ git clone ssh://chunjae@10.22.10.172:/c/Users/chunjae/repositories/my-repo.git
    Cloning into 'my-repo'...
    fatal: ''/c/Users/chunjae/repositories/my-repo.git'' does not appear to be a git repository
    fatal: Could not read from remote repository.
    
    Please make sure you have the correct access rights
    and the repository exists.
    ```
    
    Git에서 SSH를 사용하여 로컬 리포지토리에 접근하려 할 때, SSH 연결 문제로 인해 클론 작업이 실패했습니다. 이 문제는 SSH 클라이언트와 셸의 호환성 문제로 인해 발생할 수 있습니다. 이 경우, 기본 셸을 Git Bash로 설정하여 문제를 해결할 수 있습니다.
    
- **해결 방법**
    
    문제 해결을 위해 다음과 같은 PowerShell 명령어를 사용하여 OpenSSH의 기본 셸을 Git Bash로 설정합니다:
    
    [Windows OpenSSH 서버 Git저장소 Clone하기](https://medeev.tistory.com/50)
    
    ```powershell
    New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Program Files\Git\bin\bash.exe" -PropertyType String -Force
    ```
    
1. 커밋 및 푸시 테스트 (클라이언트 PC)
    1. **파일 생성 및 커밋**
        - 간단한 파일을 생성하고 Git에 커밋합니다.
            
            ```bash
            echo "Hello, Git Server" > README.md
            git add README.md
            git commit -m "Initial commit"
            ```
            
    2. **원격 저장소로 푸시**
        - 커밋된 변경 사항을 서버 PC의 원격 저장소로 푸시합니다.
            
            ```bash
            git push -u origin master
            ```
            
        - 정상적으로 푸시가 완료되면, 서버와 클라이언트 간의 Git 연동이 성공적으로 완료된 것입니다.

## 6. 서버 PC에서 Git 리포지토리 확인

리포지토리의 상태를 확인하여 최신 커밋이 `push`되었는지 확인합니다. 다음 명령어를 사용하여 커밋 로그를 확인할 수 있습니다:

```bash
git log --oneline
```

이 명령어는 커밋의 요약을 한 줄로 출력합니다. 클라이언트에서 `push`한 커밋이 리스트에 나타나야 합니다.
