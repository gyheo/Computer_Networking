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



<b>*the end point*</b>  
