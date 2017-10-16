# Introduction
> Internet이란 무엇인가?

Internet의 구조: core, edge<br/>
hosts는 각각의 end systems

Protocol은 communication을 조정하는 역할  e.g) TCP, IP, HTTP, FTP, SFTP ...

Internet "network of networks"  Internet 표준 → RFC, IETF

# * Protocol이란?
Protocol은 서로 주고 받는 메시지의 형식, 순서 등을 결정  
e.g) 각 나라의 언어 (한국어, 영어, 일본어, 중국어, 독일어, 프랑스어 ...)

# Network edge
network edge: applications and hosts  
* client/server model
* peer-peer model

network core: routers, network of networks  
network edeg는 직역 그대로 가장 자리의 어딘가에 위치  
Network는 계속해서 Exponential하게 팽창  

# TCP service[RFC 793]의 특징  
reliable, in-order byte stream data transfer  
loss가 발생했을 경우를 대비해서 acknowledgements 혹은 retransmission  
flow control : 받는 사람 기준  
congestion control : 보내는 사람 기준(network 상황 고려)  

# Network core(like blackbox)  
data를 전송하는 방식  
* circuit switching  
* packet-switching  

## Circuit Switching  
쉽게 표현하면 예약  
## Packet Switching  
독점하지 않고 '공유'해서 사용  
지금의 방식은 Circuit Switching이 아닌 Packet Switching 방식을 사용  

예제  
1 Mb/s link가 존재  
각 사용자가 활동할 때 100 kb/s  
활동 시간의 10%   
* circuit switching의 경우에는 예약해서 사용하기 때문에 10명의 사용자 가능  
* packet switching의 경우에는 예약하지 않고 제한이 없기에 많은 사용자 이용 가능  

circuit switching은 자원을 사용하지 않아 자원이 낭비될 가능성이 있고,  
packet swithching은 자원을 너무 많이 사용해서 packet delay나 loss가 발생  
e.g) 새벽에 league of legend를 이용할 때와 오후 시간에 league of legend 이용할 때  
