# SSH를 활용한 Git 서버 구성: SSHD 설치 및 연결 테스트

이 포스팅에서는 Windows 환경에서 SSH를 활용해 Git 서버를 구성하는 방법을 다룹니다. 첫 번째 단계로, Git 설치 및 OpenSSH 서버 설치, 설정, 그리고 클라이언트 PC에서 SSH 연결 테스트를 진행합니다.

## 1. Git A설치 (서버 PC)

먼저 서버 PC에 Git을 설치합니다. 다음 링크에서 설치 파일을 다운로드하여 설치를 진행합니다:

- **Git 설치 파일**: [Git-2.45.2-64-bit.exe](https://git-scm.com/download/win)

## 2. OpenSSH 설치 (서버 PC)

Windows에서 OpenSSH 서버를 설치하여 SSH 접속을 설정합니다.

### 2.1. 선택적 기능을 통한 OpenSSH 설치

1. **Windows 설정**으로 이동합니다.
2. **앱** > **선택적 기능** > **기능 추가**로 이동합니다.
3. **OpenSSH 서버**를 선택하고 설치합니다.

### 2.2. PowerShell을 통한 OpenSSH 설치

만약 2.1 방법이 동작하지 않는다면, PowerShell에서 다음 명령어를 실행하여 OpenSSH 서버를 설치할 수 있습니다:

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

### 2.3. SSH 서비스 시작 및 자동 실행 설정

PowerShell을 이용해 SSH 서비스를 시작하고, 시스템 부팅 시 자동으로 실행되도록 설정합니다:

```powershell
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automat
```

### 2.4. 방화벽 설정

SSH 포트(기본: 22번)를 열기 위해 방화벽 규칙을 추가합니다. PowerShell에서 다음 명령어를 실행합니다:

```powershell
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 
```

## 3. 클라이언트 PC에서 SSH 연결 테스트

서버 설정이 완료되었으면, 클라이언트 PC에서 SSH를 통해 서버에 접속할 수 있는지 확인합니다. 터미널에서 다음 명령어를 실행하여 연결을 테스트합니다:

```bash
ssh KimSoohyun@10.10.10.100
```

명령어를 실행하면, SSH 클라이언트는 `10.10.10.100` IP 주소를 가진 서버에 접속을 시도합니다. 접속이 성공하면, `KimSoohyun` 계정으로 서버에 로그인하여 터미널을 통해 명령을 실행할 수 있는 상태가 됩니다.

연결이 성공하면, Git 서버로 사용할 준비가 완료된 것입니다. 이제 SSH를 통해 안전하게 Git 리포지토리를 관리할 수 있습니다.
