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


<b>*the end point*</b>   
