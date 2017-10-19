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
* <b>(중요)</b> HTTP request, response를 주고 받기 위해서는 TCP connection이 필요  
* <b>(중요)</b> <b>HTTP uses TCP</b>, 처음에 클라이언트가 TCP 연결 (port# 80)  
* <b>(중요)</b> <b>HTTP is "stateless"</b>, 서버는 클라이언트 request의 정보를 기억하지 않는다  
* (server가 일일이 다 기억하면 server에게 부담 ↑)  

# * HTTP connections  
* non-persistent HTTP  
** 각각의 object마다 일일이 TCP connection 생성  
** object도 많아지면 TCP connection도 많아지기 때문에 overhead  
** 최소 2RTT + file transmission time (각각의 object 파일에 대해)  

> * RTT(Round Trip Time) : Packet을 보내고 ACK을 받기까지의 시간 (왕복시간)  

* persistent HTTP  
** 여러 개 object를 하나의 TCP connection을 통해 전송 like pipeline  
** 요즘 사용하는 HTTP는 persistent HTTP  
** 우선 2RTT에 TCP connection은 일정 시간동안 열려있으므로 non-persistent와는  
다르게 좀 더 TCP '징검다리'를 활용할 수 있음  

# Two types of HTTP messages :
* request  
* response  
* HTTP request message : ASCII(human-readable format)  

# * Uploading form input  
* POST method  
* * input is uploaded to server in entity body  
* GET method  
* * input is uploaded in URL field of request line:  

~~~~  
Q) HTTP는 statless인데 그러면 어떻게 상태 정보를 저장하지?  
A) By cookie  
~~~~  

# Cookies: keeping "state"  
1. client가 http request message를 전송
2. 만약 server에 해당 사용자의 정보가 없으면 header cookie 정보를 넣어 전달  
3. 시간이 지나도 cookie를 client가 가지고 있으면  
server "또 왔어? 널 위해 준비했어.." 하면서 service 제공  

## Cookie의 사용 목적
* authorization
* shopping carts
* recommendations
* user session state(Web email)

정리: 여러 web site들은 cookie를 바탕으로 사용자 pattern 분석  
(Big Data, Data Analysis)  


# Web caches (proxy server)  
* <b>Goal : satisfy client request without involving origin server</b>  
* <b>Computer Science에서 정말로 중요한 Chaching 개념</b>  
~~~~  
why Web caching?
1. client의 response time ↓  
2. access link의 traffic을 줄여준다 (해외로 나가는 traffic은 $)  
3. content provider 역할도 감당
~~~~  

~~~~  
예제)  
Caching example
e.g) 학교 기숙사에서 Google 해외 망으로 나가는 상황을 가정하고 생각해보기  
~~~~  

~~~~  
Q) proxy server의 문제점은 없을까?  
A) up-to-date file을 놓칠 수 있다. 그래서 특정 날짜의 파일에 대해 변화가 있을 경우  
up-to-date file을 새로 요청해서 받아온다
~~~~  
