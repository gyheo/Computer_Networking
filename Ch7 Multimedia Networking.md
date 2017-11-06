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


<b>*the end point*</b>   
