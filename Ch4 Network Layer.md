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

## Longest Prefix Match Forwarding  
* Destination-based forwarding  
  * packet은 dest IP address를 가지고 있고,  
  * Router는 longest prefix matching을 수행  
  * 자신에게 들어온 packet에 대해 확인하는 작업  

~~~~  
Q) Forwarding Table entry는 누가 만들까요~?  
A) by router  
~~~~  

# IP addressing: CIDR  
* CIDR : Classless InterDomain Routing  
  * 앞의 접두 prefix 부분 : 현재 자신이 속한 subnet에 대해 알려줌  

# (중요) Subnet  
* Subnet; 같은 prefix를 가진 device의 집합!  

~~~~
Q) Router는 IP주소를 가질까?  
A) 네! (router의 경우 여러개의 subnet에 속한 교집합 [그림 참조])  
~~~~  

# IPv6 이야기 (1996)
* IPv4 2의 32제곱 = 약 40억, IP address 이미 초과 (SmartPhone, iPad, etc..)  
* IPv6 128 bit, 2의 128제곱(전 세계의 모래알 개수보다 많은)  
* 현재 2017년인 지금도 IPv4가 우세  

~~~~  
배울점)  
* 새로운 요구사항이 나타날 때, 유연하고 동적인 protocol 필요  
* 미래를 예측하기 어렵고 섣불리 바꾸기 어렵기 때문에  
~~~~  

# Network Address Translation  
* 하나의 공인 IP address를 여러개의 IP address가 공유할 수 있도록  
  e.g., 학교, 가정에서의 무선 공유기  
~~~~
Q) 왜 NAT를 사용하는 이유?  
A) IPv4가 슬슬 한계가 와서 NAT의 trick 방식을 이용해 많은 기기들이 public IP를 사용할 수 있도록  
단, Network가 커지고 관리하기 어려운 부분이 있음  
~~~~
<b>*the end point*</b>  
