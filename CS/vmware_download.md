# VMware 및 CentOS 설치 방법(Windows)

1. Broadcom 가입 및 VMware 설치파일 다운로드

    1.1. Broadcom 공식 홈페이지에 아래 링크로 접속합니다.

    [Broadcom](https://www.broadcom.com/)
    
    1.2. "Support Portal > Register" 를 선택하여 절차에 따라 가입합니다.
    ![Image](https://github.com/user-attachments/assets/8ba793dd-71be-49f1-bce1-51d7003894cf)

    1.3. 가입 후 "Support Portal > Go To Portal" 를 선택하여 로그인합니다.![Image](https://github.com/user-attachments/assets/454c166e-f8cd-4d52-bd86-1ea317ad54b9)

    1.4. "Software > VMware Cloud Foundation > My Downloads"를 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/3a90ff28-7c89-4ee0-89e4-6485d2c36ed0)

    1.5. 우측 상단에 "pro"를 검색 후 "VMware Workstation Pro"를 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/9948d542-cbd1-4188-b796-ea234b3aff3e)

    1.6. 원하는 버전을 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/793dbf02-1a19-4e9a-9a54-20c694a5bfb5)

    1.7. 이용약관에 동의 후 다운로드 버튼을 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/c8150060-e8d7-462c-8588-6ca710adf500)

    1.8. 추가 정보를 기입 후 "Submit" 버튼을 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/0265dc01-ac43-4600-a3dc-d9b72c5494ab)

    1.9. 이전 화면에서 다시 다운로드 버튼을 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/c59c6aa5-1f44-4a99-a224-82cb76389772)

2. VMware 설치

    아래 순서에 따라 설치를 진행합니다.
    ![Image](https://github.com/user-attachments/assets/981acf08-6862-4cc4-9428-8cec1876647f)
    ![Image](https://github.com/user-attachments/assets/12039af9-b229-4ec9-882e-1e724427ee99)
    ![Image](https://github.com/user-attachments/assets/6f6bf79b-11aa-4f01-a8c8-4a2bd7c7ba55)
    ![Image](https://github.com/user-attachments/assets/30b2431c-b068-4669-85f3-5552d2c013c9)
    ![Image](https://github.com/user-attachments/assets/797f0560-d998-4b3a-a1e5-370a5f8d3d48)
    ![Image](https://github.com/user-attachments/assets/3d7fa525-1098-4093-b37b-8df843663694)
    ![Image](https://github.com/user-attachments/assets/7b0c44c6-9a60-4695-94bd-563d24798a7c)
    ![Image](https://github.com/user-attachments/assets/d8300607-20be-4e10-bb6e-a1379ac45c0b)

3. VMware 실행

    3.1. 바탕화면에 생긴 아이콘을 클릭하여 실행합니다.

    ![Image](https://github.com/user-attachments/assets/1eafb3fa-74a2-4d6f-b90d-6630e1377cea)
    
    3.2. 아래와 같이 실행되면 정상적으로 설치된 것입니다.
    ![Image](https://github.com/user-attachments/assets/672ff88b-079b-401d-b700-a7923fab9e81)


4. CentOS 설치파일 다운로드

    4.1. 아래 링크에서 ISO파일을 다운로드합니다.
         https://www.centos.org/download/
         ![Image](https://github.com/user-attachments/assets/0f108b1c-6442-4007-b935-b647feb15a9f)

5. **VMware에 CentOS 설치하기**
    
    **5.1. 가상 머신 생성**
    
    1. Create a new Virtual Machine을 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/30d1f906-a67a-4882-ac85-26203011b4ce)

    2. "Typical"을 선택한 후 다음 단계로 진행합니다.
    ![Image](https://github.com/user-attachments/assets/4351abb9-0a41-46a0-9f80-6e2592ba3a93)

    3. 설치 이미지 파일을 선택하지 않고 그대로 진행합니다.
    ![Image](https://github.com/user-attachments/assets/03af117f-ff2f-4ab5-813d-30ae3cc2146c)

    4. CentOS의 최신 버전을 선택하여 진행합니다.
    ![Image](https://github.com/user-attachments/assets/ef3b7981-d34f-4cfb-a3d3-aa81a68bdc2f)

    5. 가상 머신의 이름과 설치 경로를 지정합니다.
    ![Image](https://github.com/user-attachments/assets/9d97e426-ef05-4f5f-8193-20d470c19492)

    6. "Store virtual disk as a single file" 옵션을 선택한 후 다음 단계로 넘어갑니다.
    ![Image](https://github.com/user-attachments/assets/fee2c1b6-6cb2-4657-931d-8888a254c691)

    7. 설정 내용을 확인하고 "Finish" 버튼을 클릭하여 가상 머신을 생성합니다.
    ![Image](https://github.com/user-attachments/assets/e3f2a436-d1e0-4403-8ac3-c94e66476b63)

    **5.2. 가상 머신 설정 변경**

    1. "Edit virtual machine settings"를 선택합니다.
    ![Image](https://github.com/user-attachments/assets/f3872a75-5edb-42d2-b4f6-9f441be097da)

    2. 메모리와 CPU 성능을 조정합니다.
        - 메모리: 2GB
        - CPU: 2 * 2
    ![Image](https://github.com/user-attachments/assets/cd85e802-6b13-4cee-94b7-d97fe83b784f)

    3. "CD/DVD" 항목에서 다운로드한 CentOS ISO 파일을 선택합니다.
    ![Image](https://github.com/user-attachments/assets/c29b8a11-b53f-4689-baf8-848d7b01daff)

    **5.3. 가상 머신 실행 및 CentOS 설치**

    1. "Power on this virtual machine"을 클릭하여 가상 머신을 실행합니다.
    ![Image](https://github.com/user-attachments/assets/90e031ba-8783-4a0e-b3a6-847f76aaeccb)

    2. 부팅 후 " Install CentOS steam 10" 를 선택합니다.
    ![Image](https://github.com/user-attachments/assets/0a51f363-38fe-453b-a2aa-b32d8e4a381e)

    3. 언어 설정에서 한국어를 선택하고 "계속 진행" 을 클릭합니다.
    ![Image](https://github.com/user-attachments/assets/2ac2b537-ae21-4598-b21a-a0fecf5cd58a)

    **5.4. 설치 환경 설정**
        
    1. 네트워크 및 호스트 이름 설정
        ![Image](https://github.com/user-attachments/assets/37c03cb3-7fab-4546-95a6-8da040bc0a74) 
        - 호스트 이름을 변경 후 "적용" 버튼을 클릭합니다.
        ![Image](https://github.com/user-attachments/assets/a19b9da8-b3c4-457e-a3d3-f77374eee592)
        
    2. KDUMP 비활성화
        ![Image](https://github.com/user-attachments/assets/bd28d2a5-94bb-4fd7-81d0-c8d859a83dbc)
        - KDUMP를 비활성화합니다.
        ![Image](https://github.com/user-attachments/assets/45bf68f1-7195-4f2f-89eb-9b353dca441b)
    
        3. 사용자 계정 생성
        ![Image](https://github.com/user-attachments/assets/0935e198-09fd-4a1e-a23a-3e367103207f)
        - 사용자 계정을 생성하고 필요한 정보를 입력합니다.
        ![Image](https://github.com/user-attachments/assets/5fdcbddc-924e-4c73-a336-6c137ba0a540)
    
        4. root 계정 활성화
        ![Image](https://github.com/user-attachments/assets/3e8479b3-45f2-441e-9b10-ed823fd5b8fe)
        - root 계정을 활성화하고 비밀번호를 설정합니다.
        ![Image](https://github.com/user-attachments/assets/a51f22da-1afb-4478-b732-b7fe05f6b141)
    
    **5.5. 설치 진행 및 완료**
        - "설치 시작" 버튼을 클릭하여 설치를 진행합니다.
        ![Image](https://github.com/user-attachments/assets/8fa43566-a3bb-431d-b6c5-1bc7815f477c)
        - 설치가 완료되면 "시스템 재시작" 버튼을 클릭하여 설치를 마칩니다.
        ![Image](https://github.com/user-attachments/assets/ce79a4cd-8c09-42e7-977a-c84bbb22b9a7)
    
    **5.6. root 계정으로 로그인 및 네트워크 확인**
        1. 로그인 화면에서 "목록에 없습니까?" 를 클릭합니다.
        ![Image](https://github.com/user-attachments/assets/40495058-549e-47b3-86a6-9f598e34fd67)
        2. 사용자명에 "root" 를 입력하고 로그인합니다.
        ![Image](https://github.com/user-attachments/assets/751bef40-fe8e-406c-98dd-7acdb7bc3ee0)
        3. 명령어 확인
        - whoami 명령어를 실행하여 root 계정으로 로그인되었는지 확인합니다.
        - ping 명령어를 실행하여 네트워크가 정상적으로 연결되었는지 확인합니다.
        ![Image](https://github.com/user-attachments/assets/5c2a85fa-074f-4c17-b8e3-baec294f3709)
        
