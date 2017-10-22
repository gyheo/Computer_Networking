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
결과적으로 <b> duplicated packet이 도착할 가능성이 생김 </b>  
~~~~


<b>*the end point*</b>  
