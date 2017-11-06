# Multimedia Networking (Application Layer 이야기)

# (핵심) YouTube와 같은 서비스는 어떻게 제공할까?  

# Multimedia : audio  
* 소리는 공기를 타고 전달  
* 아날로그 신호 : 연속적    
* analog → digital  
* But, 완벽히 이루어질 수 없기 때문에 sampling을 촘촘히!  
  * e.g., MP3 : 96, 128, 160kbps (96kbps의 경우 1sec당 96,000bit)  

# Multimedia : video  
* video, sequence of images  
* digital image : array of pixels  
* encoding rate이 높을수록 고화질  

# Multimedia networking: 3 application types  
* streaming, stored audio, video  
  * streaming
  * e.g., YouTube, Netflix, Hulu
* <b>streaming live</b> audio, video
  * server에 저장된 게 X  

# Streaming stored video: (graph 확인)  
  * (중요) network delay : 유동적, 일정하지않다; jitter  
  * 위의 buffering이 길어지면 사용자에게 불편함 ㅡ_ㅡ  (YouTube의 경우)  

# Client-side buffering, playout (그림 확인)  
  * (중요) 결국, 들어오는 속도보다 playout이 더 빠를 때 buffering 발생!  

# 그럼 이 문제를 어떻게 해결할 것인가?
  * Application(e.g., YouTube, Netflix, Hulu)등은 Transport Layer 의존
  * TCP는 network상황을 통해 cwnd control을 하고, UDP는 그냥 내던지고..  

# (중요) Streaming multimedia: DASH
  * DASH : Dynamic, Adaptive Streaming over HTTP  
  * server
    * 2GB의 영상을 여러 개의 chunk로 divide  
    * 각 chunk를 저장하고 각각 다른 rate으로 encoding  
    * manifest file : 각 chunk에 대한 URL table을 제공  
  * client :  
    * 주기적으로 server와 client의 bandwidth 측정  
    * available bandwidth 내에서 자기 자신에게 알맞는 chunk request  
      * bandwidth가 좋을 때는 1080p를 요청할 수 있고,  
      * bandwidth가 좋지 않을 때에는 144p 요청할 수도 있음  

~~~~  
Q1) YouTube의 현재 사용자 수?  
A1) 억 단위의 동시 접속자 수    

Q2) 그럼 YouTube server 힘들텐데 어떻게 해결하지?  
A2) 우아하게 아름다운 Multicast (중간에서 찢어 나눠주는 but 현실적으로 구현 어려움)  
  So, Content Delivery Network; CDN을 이용  
~~~~  

# (중요) Content Delivery Network (CDN)  
  * 어떻게 사용자에게 가까운 CDN으로 request할 수 있을까?  
  * 패킷 열어서 IP 확인한 다음 근처 CDN으로, CDN domain name의 IP주소 확인할 때 DNS에게 물어본다 (처음에 local name server 확인하고 없으면 쭉쭉 따라가서 결과적으로 authorative dns server에게 물어보겠지)  
  * CDN을 어디에 설치하는 게 좋을까?  
  * 사용자 hop수에 가깝도록 access network 안에 CDN을 '딱' 설치  
  * e.g., Netflix의 경우 별도로 server운영하지 않고 클라우드와 CDN을 통해 서비스 제공  
<b>*the end point*</b>   
