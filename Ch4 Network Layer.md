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
Q) TTL?  
A) Network 상에서 죽을때까지 패킷이 돌아다닐까봐..  
~~~~  

# IP Address (IPv4)  
* 32bit 숫자 (이론상 2의 32제곱만큼 IP address를 사용)  
* interface의 확인이 가능하도록  
* 8bit씩 끊어서 표시 (12.34.156.6)  

# Hierarchical Addressing: IP prefixes  
* Network and host positions  
* 12.34.125.6/24, prefix = 접두  

# Subnet mask  
* 주소 중 어디까지가 network ID(=subnet ID, prefix) 인지 표시  
* (중요) Subnet Mask는 IP address와 늘 같이 따라다닌다  

# IP address allocation 역사  

## Classful Addressing  
* Class A: 0*, B: 10*, C: 110*에 따라 배분  

## Classless Inter-Domain Routing (CIDR)  
* host수에 따라 자유롭게 필요한 만큼!  




<b>*the end point*</b>  
