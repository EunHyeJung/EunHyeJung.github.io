---
layout: post
title:  "HTTPS(HyperText Transfer Protocol over Secure Socket)"
date:   2018-09-20
author: EunHye Jung
categories: network,server
comment : true
tags:	server network http https ssl 네트워크
cover:  "/assets/instacode.png"
---   
          
   
##  <font color = "#0E4D92"> HTTP, HTTPS</font>  
  
  ![content01](/assets/contents/network/content03_https.PNG)    
   
* `HTTP`는 웹 브라우저와 웹 서버가 데이터를 주고받을때 사용되는 통신 규칙(프로토콜)이다.  
* `HTTPS`는 HTTP에서 보안이 강화된 프로토콜(SSL로 암호화한 프로토콜)이며, SSL위에서 HTTP가 동작하는것이다.  
  HTTPS를 통해 데이터 통신시 악의적인 감청이나 데이터 변조를 방지할 수 있다.   
  	
    
- - -  
   
   
##  <font color = "#0E4D92"> SSL 디지털 인증서</font>  
   
   
* 클라이언트(웹브라우저), 서버(웹 서버)간의 통신을 제3자가 보증해주는 전자화된 문서.  
* 웹브라우저가 서버에 접속한 직후, 서버는 클라이언트에게 이 인증서를 전달한다.  
  웹 브라우저는 이 인증서 정보가 신뢰할 수 있는것인지 검증한 후 다음 절차를 수행하게 된다.  
* SSL 디지털 인증서 사용시 다음과 같은 이점이 있다.  
  1) 통신 내용이 공격자에게 노출되는 것을 막을 수 있음 : <font color="#7C0A02"> 암호화 </font>  
  2) 클라이언트가 접속하려는 서버가 신뢰할 수 있는 서버인지 판단가능 :  <font color="#7C0A02"> 위장 방지</font>   
  3) 통신 내용의 악의적인 변경 방지 가능 :  <font color="#7C0A02"> 변조 방지</font>  
  	
    
- - -  
   
    
##  <font color = "#0E4D92"> SSL에서 사용하는 암호화의 종류</font>  
  
  
### 대칭키(Symmetric-Key) 암호   
   
   
* 동일한 키로 암호화와 복호화를 같이 할 수 있는 암호화기법. (1개의 키를 사용)  
  클라이언트가 암호화키로 암호화하면 서버가 암호화키와 동일한 복호화키로 복호화함.   
* 구조가 간단하므로 상대적으로 부하가 걸리지 않음.  
* 하지만, 키를 미리 공유해둘 필요가 있기 때문에 키의 전송문제를 고려해야한다.  
  (대칭키가 유출되면 키를 획득한 공격자는 암호의 내용을 복호화 할 수 있음)  
   
    
### 공개키(Public-Key) 암호  
  
   
* 암호화와 복호화에 각각 서로 다른 키를 사용하는 암호화 방식. (2개의 키를 사용)  
  만약 A키와 B키가 존재할때, A키로 암호화 했다면 반드시 B키로 복호화해야하고, B키로 암호화하면 반드시 A키로 복호화해야한다.  
* 두개의 키 중 하나를 비공개키(Private Key, 개인키, 비밀키)로 사용하고, 나머지 하나를 공개키(Public Key)로 지정한다.  
  그리고 비공개키는 자신만 가지고, 공개키는 타인에게 공개한다. (공개키를 가진 사람이 데이터를 암호화해서 비공개키를 가진 사람에게 데이터를 전송)  
* 공개키는 '인증'시에도 사용 가능하다.  
  비밀키를 가진 사람이 자신이 가지고 있는 정보를 암호화해서 공개키를 가진 사람에게 전달한다. 그리고 정보를 전달받은 사람이 자신이 가지고 있는 공개키로 그 내용을 복호화하는 것에 성공했다면 자신이 받은 정보가 비밀키를 가진 사람이 전송한 정보라는것을 인증한 것을 의미한다.(인증서의 원리)     
  	
    
- - -  
   
      
##  <font color = "#0E4D92"> SSL 인증서</font>  
  
인증서의 기능은 크게 두가지  
1) 클라이언트가 접속한 서버가 신뢰할 수 있는 서버임을 보장.  
2) SSL 통신에 사용할 공개키를 클라이언트에게 제공.   
   (인증서에는 공개키가 들어가 있음)  
  
  
  
### CA(Certificate Authority)  
  
인증서의 역할은 클라이언트가 접속한 서버가 클라이언트가 접속하려했던 서버가 맞는지 보장하는 역할을 하는데, 어떻게 보장할 수 있는지에 이슈가 생기는데 이 역할을 전담하는 기업들이 존재.  
해당 사이트가 신뢰할 수 있는 사이트인지를 보장하는 기관, 기업들을 CA 혹은 Root Certificate라고 부름.    
CA는 엄격한 기준에 의해 선별됨.  
  
SSL를 통해서 암호호된 통신을 제공하려는 서비스는 CA를 통해 인증서를 구입해야함. CA는 서비스의 신뢰성을 다양한 방법으로 평가.     
  
  
  
### SSL 인증서의 내용  
  
` * 서비스의 정보(인증서를 발급한 CA, 서비스의 도메인 등)`   
  클라이언트가 접속한 서버가 클라이언트가 접속하려 한 서버가 맞는지에 대한 내용을 담고 있음.  
    
`* 서버 측 공개키(공개키의 내용, 공개키의 암호화 방법)`   
   서버와 통신할 때 사용될 공개키와 그 공개키의 암호화 방법들에 대한 정보가 담겨져 있음.  
   
인증서를 어떻게 클라이언트에게 전달할까 ?  
웹 브라우저가 SSL 프로토콜을 이용해 특정 서비스에 접속하게 되면, 내부적으로 서비스는 그 서비스의 인증서를 클라이언트에게 전송해준다. 이 인증서는 공인된 기관 CA에 의해 구입해서 발급된것임!  
(서버는 인증서 발급시 CA에게 서비스의 도메인, 공개키와 같은 정보를 전달한다.)  
    
  
<b> 브라우저는 CA를 이미 알고 있다! </b>    
  
브라우저는 내부적으로 CA리스트를 미리 파악하고 있다. (어떤 기관이 공인된 기관인지 가지고 있음) 
  
  
### SSL 인증서가 서비스를 보증하는 방법  
  
웹 브라우저가 서버에 접속할 때, 서버는 가장 먼저 인증서를 제공한다.  
브라우저는 서버가 제공한 인증서를 발급한 CA가 자신이 보유한 CA리스트에 있는것인지를 확인한다. 
확인 결과, 해당 인증서의 CA가 자신이 보유하고 있는 CA리스트에 포함되어 있다면, 해당 CA의 공개키를 이용해서 인증서를 복호화 한다.  
브라우저에 내장되어 있는 CA의 공개키로 인증서를 복화하는데 성공하였다면, 그 인증서가 공인된 기관에 의해 인증된 정보라는것을 확인하는 것임, 그리고 공인된 기관이 이 사이트는 믿어도되!라고 했다라는것이 내포되어있다는것임.  

  
- - -  
   
    
##  <font color = "#0E4D92"> SSL의 동작방법</font>  
  
  
<b> SSL은 암호화된 데이터를 전송하기 위해 공개키와 대칭키를 혼합하여 사용한다 </b>  
  
`실제 데이터(ex) id, paasword 정보)` : 대칭키 방식으로 암호화  
`대칭키의 키` : 공개키  
  
일반적으로 컴퓨터가 네트워크를 이용해서 통신할 때는 내부적으로 3단계에 걸쳐 이루어진다.  
 
악수(handshake) → 전송(세션) →  세션종료  
  
  
### 악수(handshake)  
  
서버와 클라이언트가 실제 데이터를 주고받기 전에 Handshake과정을 통해 서로 상대방이 존재하는지, 또 상대방과 데이터를 주고받기 위해 어떤 방법을 사용해야하는지를 파악한다. 
핸드쉐이크 과정에서 가장 중요한 작업은 바로 <b>SSL 인증서를 주고 받는 것</b>이다.  
  
<font color="#007474"><b> 핸드쉐이크 과정에서 클라이언트와 서버가 통신하는 과정 </b> </font>  
  
1) 웹브라우저가 웹 서버에 접속(클라이언트가 서버에 접속)   
  이 단계를 `Client Hello`라고 한다. 이 단계에서 주고받는 정보는 아래와 같다.  
  * 클라이언트 측에서 생성한 랜덤 데이터  
  * 클라이언트가 지원하는 암호화 방식들  
  * 세션 아이디 : 이미 SSL 핸드쉐이킹을 했다면 비용과 시간을 절약하기 위해 기존의 세션을 재활용함.  
    
2) 서버는 Client Hello에 대한 응답으로 `Server Hello`를 하게 된다. 이 단계에서 주고받는 정보는 아래와 같다.   
  * 서버측에서 생성한 랜덤 데이터  
  * 서버가 선택한 클라이언트의 암호화 방식  
  * <font color="#c21807">인증서 </font>  
  
3) 클라이언트는 서버가 전송한 인증서가 어떤 CA에 의해 발급된 인증서인지 확인.  
   해당 인증기관이 브라우저가 보유한 CA 리스트에 존재하는지를 확인.  
   브라우저에 내장되어 있는 CA 리스트에 해당 인증서를 발급한 CA가 존재한다는것은 해당 인증서에 대한 공개키를 이미 가지고 있다는 뜻임 -> 이 공개키로 인증서 복호화 시도.  
   만약, 공개키로 인증서가 복호화가 된다면 해당 인증서가 틀림없이 그 인증기관에 의해 발급된것이라는것을 브라우저는 알 수 있게 된것임 -> 자신이 접속한 서비스가 공인된 기관에서 보증된 안정적인 서비스라는것을 확신할 수 있음!   
  
  

- - -   
　 
#### 참고(Reference)   
   
[생활코딩(HTTP와 SSL 인증서)](https://opentutorials.org/course/228/4894)    
[그림 한 장으로 보는 최신 서버 가이드북](https://book.naver.com/bookdb/book_detail.nhn?bid=11433282)　  
   
   