# Network Security Solution
 
**SecuwaySSL U V2.0** 전용 장비를 이용하여, 설계된 가상 시나리오 요구 사항에 맞게  
각종 네트워크 보안 솔루션 ( FW, IDS, VPN, SNAT 등 )을 구현했습니다.  
Virtual Machine 운영체제는 모두 **Ubuntu 20.04 Desktop** 환경에서 진행하였습니다.
 
### Tools 
- Linux ( Ubuntu 20.04 Desktop )
- VMware Workstation 16
- ipTIME PoE1008 Switch - 2EA 
- SecuWiz SecuwaySSL UminiS - 2EA
### Installed packages 
- Apache2
- Wireshark
- Nmap
- hping3

### Network configuration
![image](https://user-images.githubusercontent.com/80202054/266510740-5426aec1-c4fe-4f57-94e3-8f270e81904a.png)

### List
- Firewall, SSLVPN에 대한 내부 시스템 SSH 접근 허용
- Virtual IP 생성 후 Server1에 **Static NAT**을 사용하여 1:1 매핑
- 내부 → 외부, WAN Port IP 이용하여 통신 ( **Source NAT** )
- 외부 → 내부, SYN Attack 탐지 및 로그 ( **IDS** )
- **OpenVPN** 사용하여, **SSLVPN** 설정 ( **SSL/TLS + User Auth** 인증 방식 채택 )


---
### Firewall, SSLVPN에 대한 내부 시스템 SSH 접근 허용
Firewall, SSLVPN 장비 Web GUI에서 SSH 활성화 및 root 계정 로그인 가능하도록 설정  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/5a82a3a0-3654-4618-a2a3-15e48a3f8148)  

Server2 -> Firewall SSH Test  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/6b405b2b-ee7b-4e41-b908-8b7736697a94)  

---
### Virtual IP 생성 후 Server1에 Static NAT을 사용하여 1:1 매핑
Create Virtual IP on WAN Ports  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/198318d3-d4dc-4bea-b728-9bbf9e4c9b96)  

Mapping VIP ( 210.110.10.250 ) to Server1 ( 192.168.1.100 )

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/b0e68c12-f95b-4196-8ca3-3abe0e43c789)  

Server1 -> Client Ping Test  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/9d07436a-ab89-44fb-ae8a-4f7a12a6f1e7)  

---
### 내부 → 외부, WAN Port IP 이용하여 통신 ( Source NAT )
LAN net <-> WAN net, LAN net uses WAN port IP  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/8547e8df-ca84-44b5-90c2-f56386166da5)  

Server2 -> Client Ping Test  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/2bf623d3-01d8-43bf-8665-fab1da16bb8b)  

---
### 외부 → 내부, SYN Attack 탐지 및 로그 ( IDS )
Intrusion Detection System Enable  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/5a321ba3-9c02-4fcb-b41a-10f1b5c1cfdf)  

SYN Flooding alert Rule Enable  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/6d51192a-eb20-409a-bf19-ae4330a36fc9)  

emerging-dos Ruleset Enable  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/3cae161b-7721-41ed-bfad-a670afd398b7)  

Policy Apply  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/ef827213-dfea-4d07-9b86-8d2281bc9fd7)  

SYN Flooding Test  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/3179ae6d-5635-4429-ae44-ecf3f1fb89aa)  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/c3fd3342-e18e-412c-a3c1-07d32f35d2d8)  

---
### OpenVPN 사용하여, SSLVPN 설정 ( SSL/TLS + User Auth 인증 방식 채택 )
Add Internal Authorities  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/212196d4-4fb7-4199-87ca-a043add59ffe)  

Add Server Certificate  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/bb8fc2a3-1863-4beb-b9cc-b23afca459b4)  

Add a user to use when connecting to a VPN  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/990b1bc2-e481-4071-8622-3ed73ed2578d)  
( Check this option && Save )  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/8df75e44-39da-4a96-8d56-9d2fbccbbca8)  

Add Client Certificate for ovpn user  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/7eb4e0c7-5279-4965-bc07-85c5c036b5f1)  

Create an OpenVPN server using "Use a wizard to setup a new server"  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/09194336-4246-480f-8c77-2e7ecbcf2036)  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/f21b38d2-fe7a-4194-92e4-0be8f8745818)  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/d1323b27-cf73-42b8-9fa8-ee4932c764e2)  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/cf63b631-d5d3-4f1f-8617-7741a58c9a3e)  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/d0d1e7fd-e84c-49c9-8e22-83a0f14ef41d)  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/3cf6ff6e-ab9a-411f-a736-dfa8e947e99d)  

Client Export ( ovpn File )  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/627d6066-9e75-41f9-875e-b5ee56ff7efc)  

Run ovpn file on SSLClient  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/0fa38d9b-6f35-4446-85f7-8619db629b2f)  

SSLClient -> Server1 Ping Test  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/ddd79c91-8720-4e2f-91c2-f784451331df)  
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/d2843aa4-490d-4ce5-bebc-d683719ff185)  

---
# Troubleshooting
## [ERROR] certificate is not yet valid
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/c032cde7-9ca1-4d23-8a4b-5ae3f9ef82b1)  

OpenVPN 설정 후, 처음 OpenVPN 접속을 시도했을 때 위와 같은 오류가 떴다.  
먼저 인증서와 관련된 오류이니 SSLVPN에서 만들었던 인증서를 확인해봤다.  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/b98c3369-d0a3-4773-b57e-2d43a9e1e23a)  

딱히 인증서 자체에 문제가 있어보이지는 않아, 다시 오류 메시지를 확인해보니 "yet" "아직"이라는 단어가 눈에 띈다.  
따라서 인증서의 유효 기간에 문제가 있다고 추론하고, 인증서 유효 기간과 SSLClient 시스템 시간을 확인해봤다.  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/0c820598-235c-4f55-b88c-b95670c8e52e)
![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/b553f3fc-dfeb-4ad7-a6d0-2509350bf4ed)  

위 사진을 보면 인증서 유효 기간은 2023-09-07 14:55 부터 유효하다고 나와있지만,  
SSLClient 시스템 시간은 그 전인 2023-09-06으로 설정되어 있다.  

따라서 SSLClient 시스템 시간을 인증서가 유효한 기간으로 바꾸거나, SSLVPN 시스템 시간과 동일하게 변경하면 해결되는 문제이다.  

![image](https://github.com/rkadl9999/Network_Security_Solution/assets/80202054/d4ad91bb-7b81-45fc-a887-23bf2f114408)  
( 위와 같이 시간을 변경하고 다시 연결을 시도 했을 때 연결 성공 )
