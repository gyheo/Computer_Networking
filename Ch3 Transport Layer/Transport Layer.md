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



<b>*the end point*</b>  
