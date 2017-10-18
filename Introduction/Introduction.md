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
~~~~
예제1
1 Mb/s link가 존재  
각 사용자가 활동할 때 100 kb/s  
활동 시간의 10%
~~~~
* circuit switching의 경우에는 예약해서 사용하기 때문에 10명의 사용자 가능  
* packet switching의 경우에는 예약하지 않고 제한이 없기에 많은 사용자 이용 가능  

<b>정리</b>  
circuit switching은 자원을 쓰지 않는 채 낭비될 가능성이 있고,  
packet swithching은 자원을 너무 많이 사용해서 packet delay나 loss가 발생  
e.g) 새벽에 league of legend를 이용할 때와 오후 시간에 league of legend 이용할 때  

# Internet structure: network of networks  

# Packet의 loss와 delay는 왜 발생할까?  
<b>Router buffer 안에 있는 packet들의 queue</b>  
※ 들어오는 속도가 나가는 속도보다 빠를 때 queueing 현상 발생!  

## Four sources of packet delay  
* nodal processing  
packet이 처음 들어왔을 때 처리 과정  
* queueing(variable)  
전송을 위해 output link에서 기다리는 시간  
* transmission delay  
bit를 link로 보내는 데 걸리는 시간  
e.g) 파이프에 물을 붓는 과정  
* propagation delay   
실제 거리를 빛의 속도로 나눈 시간  
~~~~
예제2  
Caravan analogy 문제 - 이해하기에 좋은 듯
~~~~
* 우리가 줄일 수 있는 요소 - queueing delay  
* processing delay는 좋은 CPU를 사용하면 줄일 수 있고  
* transmission delay는 좋은 cable 사용하면 줄일 수 있다  
* Packet Loss는 유한한 용량을 넘게 되면서 발생하는 현상

Q) 재전송은 누가 해줄까?  
A) router들이 아닌 sender (TCP 차원)    

~~~~
예제3  
windows cmd에서 tracert 실행해보기
~~~~  

# * Layering  
> Networks are Complex!  

네트워크 자체가 복잡하기 때문에 '관리'하기 쉽도록 무언가의 조치가 필요하다!  
*Internet Protocol Stack*  

# Encapsulation  
Internet Protocol Stack에서 각각의 layer를 지나갈때마다 header 추가  
각 layer 영역에서의 packet 이름을 알아두자  
application ← message  
transport ← segment  
network ← datagram  
link ← frame  

end point  
