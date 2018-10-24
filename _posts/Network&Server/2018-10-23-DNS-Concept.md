---
layout: post
title:  "DNS (Domain Name System)"
date:   2018-10-23
author: EunHye Jung
categories: network,server
comment : true
tags:	server network DNS IP  네트워크
cover:  "/assets/instacode.png"
---   
   
###   <font color="#04635b"> IP 주소 (InternetProtocol Address) </font>  
  
* 인터넷에 견결된 각각의 컴퓨터(호스트)를 구별하는데 사용.  
* 32비트 숫자를 8비트씩 4부분으로 나누고, 각 부분을 점(.)으로 구분해서 각각 10진수로 표현.  
* NIC(Network Infromation Center)에서 할당, 관리.  
   
   
###  <font color="#04635b"> 도메인 네임 (Domain Name) </font>   
   
* 사람들이 이해가기 어려운 숫자로 표현된 IP 주소에 대응되는 이름.  
   
   

###  <font color="#04635b"> URL (Uniform Resource Locator)</font>   
    
* 인터넷 상의 자원의 위치를 나타내는 문자열로서, 자원의 물리적인 주소를 나타냄.  
* 다양한 스키마를 통해 자원의 접근 수단을 제공하는 체계.    
  
  
###  <font color="#04635b"> URI (Uniform Resource Idenfitier)</font>   
    
* 통합 자원 식별자.  
* 인터넷 상의 정보자원에 대한 식별체계      
* URI의 하위 개념으로 URL과 URN이 있음.  
* 예를 들어, `https://www.google.com/`라는 주소는 URL이면서 URI이다.  
  `https://eunhyejung.github.io/network,server/2018/10/09/Osi7Layer-Concept.html`는 eunhyejung.io 호스트 주소 하위에 network,server/2018/10/09라는 디렉토리 아래에 Osi7Layer-Conecpt.html라는 자원의 위치를 가리키고 있으므로 URL이면서 URI이다.  
구글에서 'github'이라고 검색을 하게 되면 `https://www.google.co.kr/search?q=github` 와 같은 형태의 URL을 확인할 수 있다. 여기서 q=github 부분은 검색에어 따라 유동적으로 변경되는 값이다. 이 주소에서 URL은 https://www.google.co.kr/search까지이고, 원하는 정보를 얻기 위해 q=github라는 식별자가 필요하다. 그러므로 https://www.google.co.kr/search?q=github이 주소는 URI이지만 URL은 아니다.  
  
   
- - -    
   
   
##  <font color = "#0E4D92"> DNS (Domain Name System) </font>  
   
   
* 사람이 읽을 수 있는 <b>도메인 이름(ex) www.naver.com)</b>을 컴퓨터가 읽을 수 있는 <b>IP 주소(ex) 125.209.222.142)</b>로 변환하는 서비스를 제공.  
* 전화 안내 서비스인 114와 비슷한 역할을 한다고 보면됨!   
   
   
- - -   
   
   
##  <font color = "#0E4D92"> IP 주소를 얻기 위한 내부 흐름 </font>  
  
* 사용자가 브라우저 주소창에 도메인을 입력하면 브라우저는 그 도메인에 해당하는 IP 주소를 찾기위해 DNS 서버에 접속한다.  
  DNS 서버는 도메인에 대한 IP 주소를 알려준다.  
  IP 주소를 획득한 브라우저는 인터넷을 통해 IP 주소에 해당하는 컴퓨터에게 사용자가 요청한 웹페이지를 요청한다.  
  (서버 컴퓨터에서 이러한 요청을 처리해서 응답을 담당하는 것이 바로 웹서버)  
  웹 서버는 요청한 웹페이지를 사용자에게 전달하고, 사용자 화면에 요청된 결과물의 웹페이지가 표시된다.  
  
  
  ![content01](/assets/contents/network/content04_dns.PNG)    
  
  
* 일반적인 컴퓨터에서 정상적으로 인터넷이 작동하는 상태는 1, 2, 4, 7, 8, 9 , 3의 과정을 거치게 된다. 
* DNS서버는 약간 독특한 방식으로 IP 정보를 알려준다.  
  세상에는 정말 많은 도메인이 있으며, 한대의 DNS 서버에 모든 주소를 저장하는 것은 불가능하다.  
  도메인에 따른 IP주소들은 전세계의 DNS 서버에 흩어져 있어서, 정해진 규칙에 따라 IP 주소를 제공하게 된다.   
   
  
- - -  
   
   
[참고 - DNS의 원리(https://opentutorials.org/course/3276/20299)](https://opentutorials.org/course/3276/20299)   
[참고 - DNS구성요소(http://library.gabia.com/contents/domain/4137)](http://library.gabia.com/contents/domain/4137)     
   
    