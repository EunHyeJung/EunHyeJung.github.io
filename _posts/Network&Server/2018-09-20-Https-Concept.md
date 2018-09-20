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
　 
#### 참고(Reference)   
   
[생활코딩(HTTP와 SSL 인증서)](https://opentutorials.org/course/228/4894)    
[그림 한 장으로 보는 최신 서버 가이드북](https://book.naver.com/bookdb/book_detail.nhn?bid=11433282)　  
   
   