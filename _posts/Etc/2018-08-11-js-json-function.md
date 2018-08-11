---
layout: post
title:  "JS-JSON.parse(), JSON.stringify()"
date:   2018-08-11
author: EunHye Jung
categories: etc
comment : true
tags:	js javascript
cover:  "/assets/instacode.png"
---   
    
      
- - -      
   
[참조](https://www.w3schools.com/js/js_json_parse.asp)   
   
- - -    
  
  
###  <font color = "#0E4D92"> JSON.parse() </font>    
  
  
* 웹서버로부터 데이터를 받을때, 데이터는 항상 문자열(string) 형태이다.  
  `JSON.parse()`를 이용해서 데이터를 파싱하면, 데이터는 자바스크립트 객체가 된다.  
* `JSON.parse()` 지원 브라우저  
   * Firefox 3.5  
   * Internet Explorer 8  
   * Chrome  
   * Opera10  
   * Safari4  
   
  
_ _ _   
  
   
#### <font color="#212930">  Example </font>     
  
* 다음과 같은 형태를 웹서버로부터 받았다고 하면,  
  
  `'{ "name":"John", "age":30, "city":"New York"}'`   
  
  자바스크립트 함수 JSON.parse()를 사용해서 텍스트를 자바스크립트 객체로 변환한다.   
  
  ```javascript  
  var obj = JSON.parse({ "name":"John", "age":30, "city":"New York"}');
  ```   
  
  

- - -    
  
  
###  <font color = "#0E4D92"> JSON.stringify() </font>    
  
  
* JSON형태로 데이터를 서버와 주고받을때, 웹서버로 데이터를 보낼때, 데이터는 문자열(string)형태여야 한다.  
* 자바스크립트 객체를 문자열의 형태로 바꾸기 위해서는 `JSON.stringify()`함수를 이용한다.  
* `JSON.stringify()` 지원 브라우저  
   * Firefox 3.5  
   * Internet Explorer 8  
   * Chrome  
   * Opera10  
   * Safari4  
   
_ _ _   
  
   
#### <font color="#212930">  Example </font>     
  
* 다음과 같이 <b> obj </b> 객체 변수를 웹서버에 보내려면,  
  
  ```javascript
  var obj = { name: "John", age: 30, city: "New York" };
  ```   
  
  `JSON.stringify()` 함수를 사용하면 된다.  
  
  ```javascript  
  var myJSON = JSON.strinigfy(obj);  
  ```   
  
  
  
