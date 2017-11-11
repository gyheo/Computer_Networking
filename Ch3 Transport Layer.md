# Transport Layer  
Goal : provide logical communicaiton

# Transport vs. network layer  
* network layer : host간의 logical communication  
* transport layer : process간의 logical communication  

# Internet transport-layer protocol  
* reliable, in-order delivery (TCP)  
  * 많은 기능을 제공  
  * (sender view) congestion control  
  * (receiver view) flow control  
  * connection setup  

* unreliable, unordered delivery: UDP   
  * 많은 기능을 제공하지 않음 (가벼움)  

# * Multiplexing/demultiplexing  
* Multiplexing  
  * 여러개에서 하나로  
  * connection-oriented demux → TCP socket identified by four-tuple  
  (src IP address, src port #, dest IP address, dest port #)  
  * Web servers have different sockets for each connecting client  
  (non-persistent will have different socket for each request)  
* Demultiplexing  
  * 하나에서 여러개로  
  * connectionless demux → UDP socket identified by two-tule  
  (dest IP address, dest port #)  

# UDP: User Datagram Protocol [RFC 768]  
* "no frills" "bare bones" Internet transport protocol  
* "best effort" service, UDP segments may be:
  * lost
  * delivered out of order to app  
* <b>connectionless</b>:
  * no handshaking between UDP sender, receiver  

~~~~
Q) 왜 UDP를 사용하는가?  
* no connection establishment → delay 감소 효과  
* simple: no connection state at sender, receiver  
* header가 단순하고 크기가 작음  
* <b>no congestion control</b>  
~~~~  

## UDP: more  
* 주로 multimedia streaming application에서 사용
  * loss tolerant  
  * rate sensitive  

* other UDP uses  
  * DNS  
  * SNMP  

* error 확인을 위한 checksum 기능 제공 in header (16 bit)  

~~~~
Q) unreliable한 상황에서 발생할 수 있는 문제에 뭐가 있을까?
A) Message error, Message loss  
~~~~  

# Let's Build simple Reliable Data Transfer Protocol!  
## TCP 설계를 위한 RDT version series  
* incrementally develop sender, receiver sides of reliable  
data transfer protocol (rdt)

# Rdt1.0: Data Transfer over a Perfect Channel  
* Perfectly reliable (진공상태?)
  * no packet errors  
  * no packet loss  
* Underlying channel is reliable!  

# Rdt2.0: Channel with packet errors (no loss)  
* error를 방지하기위한 방법에 무엇이 있을까?
  * Error detection  
    * checksum bit 추가

  * Feedback
    * (중요) Acknowledgements (ACKS) : receiver측에서 "잘 받았어!" 라고  
    명시적으로 sender에게 알려줌  
    * Negative acknoledgements (NAKs) : receiver측에서 "패킷 error 있어!" 라고  
    명시적으로 sender에게 알려줌

  * Retransmission  
    * sender가 NAK에 대응하는 packet을 재전송  

~~~~
Q) rdt2.0: error를 완벽히 처리할 수 있을까?  
A) ACK 혹은 NACK에서 error가 발생하는 경우에는..?  
결과적으로 duplicated packet이 도착할 가능성이 생김
~~~~

# 중복되는 packet 처리 (rdt2.0 문제점 극복)   
* sender 측에서 각 packet에 <b>sequence number</b> 추가  
* ACK 혹은 NAK이 왜곡된 경우 sender에서 retransmit  
* receiver의 경우 duplicate packet은 버린다  

# rdt2.1: packet error
* sender
  * packet에 seq # 추가  
  * 받은 ACK/NAK이 왜곡되었는지 반드시 확인  
  * NAK 혹은 왜곡된 ACK에 대해 retransmit  

* receiver  
  * packet이 duplicate 되었는지 반드시 확인  
  * 받은 packet이 잘못된 겨우 NAK 전송  

# rdt2.2: a NAK-free protocol  
* rdt2.1과 비슷하지만 using ACKs only  
* NAK 대신 ACK # 마지막에 제대로 받은 number 표시  
* Duplicated ACK이 오는 경우에는 NAK을 받고 재전송하듯이 행동  

# rdt3.0: <b>channel with loss</b> & packet errors  
* packet loss가 발생했을 때 어떤 mechanisms을 취할 것인가?  
  * 보낼때마다 Timer  
* sender는 ACK을 "적절하게" 시간을 가지고 기다림  
* 만약에 packet (혹은 ACK)이 지연되는 경우 (not loss) :  
  * retransmission은 중복되지만 seq. #로 조절 가능 (중복된 packet은 discard)  

## Recap: Principles of Reliable Data Transfer  
* unreliable channel에서 발생할 수 있는 문제
  * (중요) packet error, packet loss  
* packet error 대처 방법  
  * Error detection, feedback, retransmission, sequence #  
* packet loss 대처 방법  
  * Timeout!  
* (중요) We build simple reliable data transfer protocol  
  * Real-world protocol (e.g., TCP) is more complex,  
  but with same principles!  

# Performance of rdt3.0; 신뢰성 보장  
* performance stinks because of <b>stop-and-wait operation</b>  
* e.g., 고속도로 16차선에 차 1대만 있는 상황  

# Pipelined protocols  
* Pipelining : sender allows multiple, "in-flight", yet-to-be-  
acknowledged pkts  
  * seq # 증가  
  * buffering at sender and/or receiver  

  * Two generic forms of pipelined protocols:  
  (방식이 아닌 Approach)
    * (중요) go-Back-N
    * (중요) selective repeat

# Pipelining: increased utilization  
> 기존의 stop-and-wait의 방식을 단점을 극복하기 위한 방법

# Go-Back-N  
* 쏟아부을것이다, 얼만큼? by window  
* (중요) cumulative ACK 이용  
e.g., "ACK 11, 나 11번까지는 완벽히 잘 받았어"  
* (중요) loss가 발생한 이후부터 받은 pkt은 discard, 최근까지 받은 pkt ACK 전송  
* timer 터지는 순간 재전송  
* 하나 loss발생해서 다른 것도 다 버리는.. (비효율적인 측면 有)  

# Selective Repeat  
* receiver가 받은 모든 packet에 대해 일일이 ACK  
* sender는 오로지 ACK을 받지 않은 pkt들에 대해 재전송  
* receiver는 packet을 갖고 있어야 할 공간 필요 (receive buffer 有)  
* Each timer  

~~~~  
+plus)
Q) receive buffer만 존재하는가?
A) 당연히 send buffer도 존재!
~~~~  

## (중요) Selective repeat in action 동작 익히기  

## Selective repeat: dilemma  
* seq # 의 한계  
(receiver측에서의 착각)  
* Solution : 0, 1, 2, 3, 4, 5, 6 seq# 늘리기  
(새로운 packet과 duplicated 구분)  

# * (중요) TCP: Overview
* point-to-point:  
one sender, one receiver(프로세스와 프로세스)  
  * socket 한 쌍 끼리    
* reliable, in-order byte stream  
  * "하나도 유실되지 않고 순서대로 간다"  
* pipelined:  
  * TCP congestion and flow control set window size  
* (중요) send & receive buffers  
  * 내보내기 전 buffer  
  * 내보낼 때 buffer에 있는 packet들을 cwnd 크기만큼 내보낸다  
  * receive buffer : out-of-order, 순서대로 도착하지 않았을 때 reordering을 위해      
* full duplex data:
  * bi-directional data flow in same connection  
  * MSS : maximum segment size  
* connection-oriented  
  * handshaking  
* flow controlled:  
  * sender는 receiver의 상태를 고려해서  
  e.g.,  sender는 슈퍼 컴퓨터, receiver는 386 컴퓨터  

# (중요) TCP segment structure  
* Protocol은 hdr가 有  

# TCP seq. #'s and  ACKs  
* Seq. #'s:
  * byte stream "number" of first byte in segment's data  
* ACKs:  
  * seq # of next byte expected from other side  
  * (중요) cumulative ACK  
    e,g,. ACK 10, receiver 曰 "10번 내놔!"  

# Timeout -- funtion of RTT  
* Timer의 시간 어떻게 정하지?  
* 네트워크 환경이 계속해서 실시간으로 변함에 따라,  
RTT도 계속 바뀔 수 有  

# TCP : reliable data transfer  
* 지금까지 배웠던 Approach 적용  
* Pipelined segments  
* Cumulative ACKs  
* TCP는 single retransmission timer 사용  
(GBN의 경우 window의 내용 모두 재전송)  

* Retransmission이 발생하는 경우  
  * timeout event 발생  
  * duplicate acks  
~~~~
Q) RTT estimation은 어떻게 이루어질까?  
A) Exponential Weighted Moving Average 이용  
(과거 값을 많이 반영할 지, 현재 값을 많이 반영할 지는 a에 의해 결정)  
~~~~  

* 예측한 RTT 값과 표준편차값을 이용해서 Timer의 value도 결정  

# Congestion Control  

<b>*the end point*</b>  
