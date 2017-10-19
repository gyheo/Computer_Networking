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

# TCP service  
* <b>connection oriented</b>  
* reliable transport  
* flow control (receiver view)  
* congestion control (sender view)  

# UDP service  
* unreliable transport   

~~~~  
생각해보기)   
sender와 receiver가 서로 통신하고 있는 경우,  
sender의 socket과 receiver의 socket이 같은 transport protocol 사용해야 함  
e.g) sender TCP socket, receiver UDP socket (X)
~~~~  

# * Web & HTTP  
* web page는 여러개의 object들로 구성  
e.g) txt, hyperlink, media(image, audio ..) ..  
* web page consists of base HTML-file  
e.g) www.someschool.com (여기까지 host name) / someDept/pic.gif(path name)  

# HTTP overview  
* HTTP : Hypertext Transfer Protocol  
e.g) http://www.google.com  
* client는 server에게 request를 날리고,  
server는 response에 object들을 실어서 client에게 response 전송  
* * HTTP request, response를 주고 받기 위해서는 TCP connection이 필요  
* * <b>HTTP uses TCP</b>, 처음에 클라이언트가 TCP 연결 (port# 80)  
* * <b>HTTP is "stateless"</b>, 서버는 클라이언트 request의 정보를 기억하지 않는다  
* (server가 일일이 다 기억하면 server에게 부담 ↑)
