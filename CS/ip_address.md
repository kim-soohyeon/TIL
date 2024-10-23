# [네트워크] IP 주소

- **IP 주소(Internet Protocol adress)**
    - 네트워크에 연결된 각 컴퓨터를 구분하는 유일한 주소로, 인터넷이나 로컬 네트워크 상에서 장치들이 서로를 찾아 소통할 수 있게 해줍니다.
- **IPv4(Internet Protocol Version 4)**
    - 4바이트 주소 체계를 사용하며, 점으로 구분된 네 개의 10진수로 나타냅니다 (예: 192.168.0.1)
- **IPv6(Internet Protocol Version 6)**
    - 네트워크에 연결된 장치가 급증함에 따라, 더 많은 주소 공간을 제공하기 위해 IPv6가 도입되었습니다. IPv6는 16바이트 주소 체계를 사용하여 더 많은 주소를 할당할 수 있습니다.
- **네이버 IP 주소 조회하기**
아래 명령어를 사용하여 네이버의 IP 주소를 확인할 수 있습니다.
    
    ```powershell
    > nslookup www.naver.com
    서버:    dns.google
    Address:  8.8.8.8
    
    권한 없는 응답:
    이름:    e6030.a.akamaiedge.net
    Address:  23.51.28.215
    Aliases:  www.naver.com
              www.naver.com.nheos.com
              www.naver.com.edgekey.net
    ```
