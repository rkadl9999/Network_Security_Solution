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
