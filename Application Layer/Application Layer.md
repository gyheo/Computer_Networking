# Application Layer  
Application Layer에는 다양한 Protocol이 존재  
e.g) FTP, HTTP, SMTP, IMAP, POP3 ...  

Application architectures
* client-server  
* peer-to-peer  

# Client-server architecture  
* server  
언제 어디서나 접속이 가능  
e.g) Google이 갑자기 접속 안되는 일이 X  
permanent IP address  

* client  
서버에게 접속하는 user들  
e.g) ssh 이용해서 서버 접속하는 경우 생각해보기  
dynamic IP address → intermittent  

# P2P architecture  
고정된 서버가 존재하지 않음  
peer는 근처의 다른 peer에게 request 요청 → self scalability  
peer와 peer의 관계는 business 관계  
(자기 일 끝나면 그냥 빠져도 됨)    

# Processes communicating  
process : program running within a host  

~~~~  
plus)  
Inter Process Communication (IPC)  
process와 process간의 통신 defined by OS
~~~~  

client process : process that initiates communication  
server process : process that waits to be contacted  

# * Sockets  
프로세스는 socket을 통해서 message를 서로 주고 받을 수 있다.
Socket을 현실 세계에 비유하자면 일종의 문  
* application 개발자는 밑의 transport나 network layer에 관해 일일이 다 알지 않아도 됨  
IP address + PortNumber → Socket에 필요  

# Application Layer protocol defines  
* types of messages exchanged  
e.g.) request, response  
* message syntax  
what fields in messages & how fields are delineated  
* message semantics  
meaning of information in fields  
* open protocols  
defined in RFCs  
e.g.) HTTP, SMTP  

# Application에서 필요한 transport service?  
(사용자 관점에서 당연한 이야기)  
* Data integrity  
<b>reliable data transfer</b>  
video의 경우 delay tolerant  
* Timing  
내가 보낸 packet이 제 시간에 도착  
e.g) 문자 메시지 보냈는데 도착이 늦는 경우 → 사용자 불편해짐  
* Throughput  
처리량, 양
* Security  
encryption, data integrity  
