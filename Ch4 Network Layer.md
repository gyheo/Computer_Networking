# Network Layer  

## Chapter goals:
* 네트워크 레이어 구조    
* forwarding과 routing의 차이  
* router가 어떻게 동작하는지?  
* routing(path selection)  
* broadcast, multicast  

# Network Layer  
* router는 일반적으로 physical, data link, network layer로 구성  
* transport에서 내려온 segment에 header를 추가 → packet명 datagram  

# * Two key network-layer functions  
* forwarding : move packets from router's input to appropriate router output  
* routing : determine route taken by packets from source to dest  

# * Longest prefix matching  
* router의 forwarding table을 확인할 때 앞의 prefix(접두)를 확인하는 방법  

# * IP datagram format  
* header 성분을 일일이 외우는 게 아니라 어떻게 구성되어 있는지 '이해'  

~~~~
Q) 얼마만큼의 overhead?  
A) 20 bytes of TCP, 20 bytes of IP = 40 bytes + app layer overhead!  
~~~~  

# (con't) IP datagram format  


<b>*the end point*</b>  
