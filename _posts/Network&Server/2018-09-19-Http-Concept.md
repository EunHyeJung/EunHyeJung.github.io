---
layout: post
title:  "WEB-HTTP(RequestMessage & ResponseMessage)"
date:   2018-09-19
author: EunHye Jung
categories: network,server
comment : true
tags:	server network http
cover:  "/assets/instacode.png"
---   
          
   
##  <font color = "#0E4D92"> 웹 구성요소 </font>     

웹페이지를 만들어주는 <b> HTML </b>   
원하는 웹페지에 방문하도록 도와주는 주소체계인 <b>URL(Uniform Resource Locator)</b>   
웹페이지를 주고받는 소프트웨어인 <b> Web browser, Web server</b>  
웹브라우저와 웹서버가 통신할때 사용하는 통신 규칙인 <b>HTTP</b>   
        
- - -   
          
## <font color = "#0E4D92"> HTTP (HyperText Transfer Protocol)  </font>  
 
웹 서버와 웹 클라이언트 사이에서 데이터를 주고받을 때 사용되는 통신규칙  
* 웹 브라우저는 웹 서버에 접근할때 메서드(Method)와 URL을 보낸다. (Request Message)  
  메서드는 서버에 대해 무엇을 하고 싶은지를 나타내는데, 일반적으로 데이터를 받고 싶은 경우 GET, 데이터를 보내고 싶은 경우 POST를 사용.    
  
HTTP는 Request와 Response를 위한 메시지로 구분되어 있다.    
  
　  
- - -  
    
##  <font color = "#0E4D92"> Reqeust Message </font>    
  
     
Request Header와 Request Body는 중간에 빈 줄(Blank Line)으로 구분한다!  
  
  
  ![content01](/assets/contents/network/content01_httprequestmsg.PNG)    
  
  
### Request Line   
   
` GET /content1.html HTTP/1.1 `   
  
<b>GET</b> : HTTP Method를 나타냄, 서버로부터 데이터를 가져올때 GET 사용    
<b>/content1.html</b> : 웹서버에 요청하는 정보를 나타냄  
<b>HTTP/1.1</b> : 웹브라우저게 현재 사용하고 있는(사용할 수 있는) HTTP 버전이 1.1이라는 뜻.  
   
   
### Request Headers  
   
`Host : www.httpstduy.com`   
  
Request Header에서 Host는 반드시 적어야함(필수), 
Host는 인터넷에 연결되어 있는 컴퓨터 한대한대를 식별하는 이름(웹 사이트의 주소)   
  
`UserAgent`는 웹 브라우저의 다른 표현, 요청하는 웹브라우저가 어떤 웹 브라우저인지를 나타냄.  
네이버에 접속해서 개발자 도구를 통해 웹 브라우저를 확인하니 아래와 같은 정보를 확인할 수 있었다.      
<i> user-agent: Mozilla/5.0 (Windows NT 6.2; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36  </i>  
Windows NT 6.2; Win64; x64은 내가 사용중인 운영체제가 윈도우이고이고 64비트 CPU라는 정보를 나타낸다.   
웹 서버 운영중에 통계를 낼때, 이 서비스에는 어떤 브라우저를 쓰는 사람들이 많이 접속하는지, 어떤 OS를 사용하고 있는지 등의 정보를 이용할 수 있게된다.    
또한, UserAgent정보를 통해 일반적인 크롬이나 파이어폭스가 아닌 검색엔진 로봇이 접속하는경우 차단할 수도 있다. (잘못된 접근 방지 가능!)  
  
웹브라우저와 웹서버가 통신할때, 응답할 데이터의 양이 클 경우 압축하여 전송하면 웹 브라우저가 그 압축을 풀어서 처리할 수 있다. 이런 방식을 이용하면 네트워크 자원을 절약할 수 있다. 그 때, 이 웹브라우저가 어떤 압축방식을 지원하는지를 나타낼때 `Accept-Encoding`을 사용한다.  
위에서 Accept-Encoding의 값으로 <i>gzip, deflate</i>으로 명시되었으므로, 웹 서버는 여기에 명시된 값중 하나의 방식으로 데이터를 보내주게 된다.  
  
동일한 페이지리를 요청할 때, 매번 그 페이지를 다운로드 받는것은 효율적이지 못하다. 이때, If-Modified-Since가 사용된다. `If-Modified-Since`는 마지막으로 해당 페이지를 언제 다운로드받은것인지를 나타낸다. 웹 서버가 응답할때, 자신이 가지고 있는 파일과 If-Modified-Since에 적힌 날짜중에 뭐가 더 최신인지를 비교해서 더 최신이 아닐 경우 페이지를 또다시 전송하지 않는다.      
  
　  
- - -  
    
##  <font color = "#0E4D92"> Response Message </font>    
  
Response Header와 Response Body는 중간에 빈 줄(Blank Line)으로 구분한다!  
  
  
  ![content02](/assets/contents/network/content02_http_responsemsg.PNG)    
  
  
Status Line은 HTTP버전과 응답 코드값을 포함한다. 
  
`Content-Type : text/html`은 웹 서버가 응답할때, 해당 응답이 텍스트이고 html라는 컴퓨터 언어라는것을 나타내고, 웹 브라우저는 이것을 보고 html라고 해석해서 화면에 표시함.   
  
`Content-Length`는 응답하는 컨텐츠의 전체 크기가 1434 (byte)라는 것을 나타냄.  
  
`Content-Encoding` 해당 컨텐츠의 압축방식을 나타냄. 클라이언트는 여기에 명시된 방식으로 압축을 풀어서 화면에 나타냄.    
   
`Last-Modified`는 이 정보가 마지막으로 수정되었는지를 알려줌.  
  
HTTP 프토로콜은 연결 상태를 유지하지 않는 <b>Connectionless</b> 구조이다. 서버에 접속하기 위해 매번 연결을 맺었다 끊었다 하는건 자원의 낭비이므로 이것을 개선하기 위해 HTTP 1.1부터 `Keep-Alive`기능이 지원된다.  
`Keep-Alive`는 통신이 연결된 소켓에 마지막으로 접근한 시점부터 일정한 시간(Time Out)이 지나기 전까지 접속상태를 유지하는것을 지원한다.  
timeout값은 커넥션 유지시간을 나타내고 max는 최대요청개수를 제한할때 사용  
   
　
- - -
    
### HTTP STATUS CODE   
  
  
* <b> 1XX (조건부 응답)</b> : 요청을 받았으며 작업을 계속  
  `100(계속)` : 요청자는 요청을 계속해야함. 서버는 이 응답코드를 통해 요청의 첫번째 부분을 받았으며 나머지를 기다리고 있음을 나타냄.  
  `101(프로토콜 전환)` : 요청자가 서버에 프로토콜 전환을 요청했으며, 서버는 이를 승인하는중을 나타냄.  
 `102(처리)`  
  
* <b> 2XX (성공) </b>  
  `200(성공)` : 서버가 요청을 제대로 처리함.  
  `201(작성됨)` : 성공적으로 요청되었으며 서버가 새 리소스를 작성.  
  
* <b> 3XX (리다이렉션 완료) </b>  
  `304(수정되지 않음)` : 마지막 요청 이후 요청한 페이지는 수정되지 않음. 
  
* <b> 4XX (요청오류) </b> : 클라이언트에 오류가 있음을 나타냄    
  `400(잘못된 요청)` : 서버가 요청 구문을 인식하지 못함.   
  `401(권한없음)` : 인증이 제대로 되지 않았을 경우 발생  
  `403(Forbidden, 금지됨)` : 서버가 요청 거부, 사용자가 리소스에 대한 권한을 가지고 있지 않은 경우 발생 (401은 인증실패, 403은 인가실패라고 봄)  
  `404(Not Found, 찾을 수 없음)` : 서버가 요청한 페이지를 찾을 수 없음, 존재하지 않은 페이지에 요청이 있을 경우  
    
* <b> 5XX (서버오류) </b>    
  `500(내부 서버 오류)` : 서버에 오류가 발생하여 요청 수행 불가.    
  `501(구현되지 않음)` : 서버에 요청을 수행할 수 있는 기능이 없음, 서버가 요청 메소드를 인식할 수 없을때.  
  
더 자세한 내용은 [위키피디아 HTTP 상태코드](https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C) 참고  
  
  
    
- - -   
　 
   
[참고 : 생활코딩(WEB2-HTTP)](https://www.youtube.com/watch?v=t7ASgtJoVz4&index=1&list=PLuHgQVnccGMBd-v_DjNm61EBaDpYZSV1Z)    
　  
   
   
      
