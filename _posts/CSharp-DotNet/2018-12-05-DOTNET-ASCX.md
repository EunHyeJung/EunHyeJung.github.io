---
layout: post
title:  "ASP.NET User Control(ASCX), Master Page"
date:   2018-12-05
author: EunHye Jung
categories: csharp,dotnet
comment : true
tags: csharp dotnet asp.net richcontrol
cover:  "/assets/instacode.png"
---  
   
## <font color = "#0E4D92"> 웹 폼 사용자 정의 컨트롤 </font>    
     
웹 폼 사용자 정의 컨트롤(User Control)은 웹페이지에서 반복적으로 사용되는 부분을 따로 파일로 구성해 사이트를 만들때 효율성을 높여준다.  
웹 폼 페이지가 ASPX 파일을 사용한다면 웹 사용자 정의 컨트롤 페이지는 ASCX 파일을 사용한다.  
웹 폼이 한 페이지 전체를 가리킨다면 웹 사용자 정의 컨트롤은 웹 폼에 올라갈 부분 페이지를 나타낸다.  
웹 사용자 정의 컨트롤은 단독으로 실행되지 않으며 반드시 웹 폼에서 실행되어야 한다.  
      
- - -   
     
     
## <font color="#04635b"> 마스터 페이지 (Master Page) </font>   
    
마스터 페이지는 사용자 정의 컨트롤을 사용한 템플릿 페이지와 같이 웹 페이지 전체에 공통적으로 사용되는 뼈대를 구성할 때 사용한다.  
마스터 페이지는 확장자가 `*.matser`이며, ASP.NET 웹 폼의 Page 지시문 대신, 아래와 같이 Master 지시문을 사용한다.    
   
```aspx  
<%@ Master Language="C#" AutoEventWireup="true" CodeBehind="Site.master.cs" Inherits="MemoEngine.Site" %>
```   
   
마스터 페이지에는 HTML, BODY 등의 일반적인 태그가 있으며, 마스터 페이지를 상속받을 각각의 웹 폼 페이지에서 적용할 내용은 다음과 같이 ContentPlaceHolder 영역을 지정해서 사용한다.   
다음 예시는 헤더, 메인, 푸터 영역이 들어오는 곳을 설정할 때의 태그모양이다.  
   
```aspx    
<asp:ContentPlaceHolder ID="HeaderContent" runat="server"> </asp:ContentPlaceHolder>
<asp:ContentPlacehHolder ID="MainContent" runat="server"> </asp:ContentPlaceHolder>
<asp:ContentPlaceHolder ID="FooterContent" runat="server"> </asp:ContentPlaceHolder> 
```    
    
다음 예시는 Default.aspx 같은 웹 폼 페이지에서 마스터페이지를 적용할 때 사용하는 지시문에 대한 코드이다.  
MasterPageFile 속성에 마스터 페이지의 경로를 지정한다.  
   
```aspx   
<%@ Page Title="메모엔진" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="Default" %>
````
     
     
- - -  
   
[참고(ASP.NET & Core를 다루는 기술 )](https://book.naver.com/bookdb/book_detail.nhn?bid=11184768)    
     
     
     
