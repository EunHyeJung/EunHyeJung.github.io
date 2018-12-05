---
layout: post
title:  "ASP.NET 상태 관리(State Management)"
date:   2018-12-05
author: EunHye Jung
categories: csharp,dotnet
comment : true
tags: csharp dotnet asp.net session cookie
cover:  "/assets/instacode.png"
---  
   
## <font color = "#0E4D92"> ASP.NET 상태 관리 기법  </font>       
   
ASP.NET에서 제공하는 상태 관리 기능은 클라이언측과 서버측 두가지로 나뉜다.  
    
<b> 클라이언트 측 상태 관리 기법 </b>  
* Hidden Field   
* View State  
* Cookies  
* Control State  
* Query Strings  

<b> 서버 측 상태 관리 기법 </b>   
* Session  
* Application  
    
     
- - -   
      
        
### Global.asax 파일  
    
Global.asax 파일은 <b>전역 응용 프로그램 클래스</b>라고 한다.  
웹 프로젝트 루트에 위치하며 웹 사이트에 처음으로 사용자가 들어올 때, 각각의 사용자가 들어올 때와 나갈때, 최종적으로 마지막 사용자가 나갈 때 등에 대한 정보를 얻어 이에 대한 후속 조치 기능을 구현할 수 있는 이벤트를 제공한다.   
Global.asax 파일은 Application과 Session 레벨 이벤트를 제공하며 주요 이벤트는 다음과 같다.  
  
* Application_Start : 웹 프로젝트 기동 후 처음으로 사용자가 방문했을 때 발생   
* Application_End : 웹 프로젝트 기동 후 마지막 사용자가 나간 후 발생, 일반적으로 마지막 사용자의 최종 요청이 끝난 후 20분 뒤에 발생  
* Session_Start :  각각 사용자가 방문할 때 발생  
* Session_End : 각각 사용자가 나가고 20분 후에 발생  
    
<b> 웹사이트의 현재 접속자수 구하기 </b>     
1) Application_Start 이벤트에서는 CurrenctVisit이라는 이름으로 Application 전역변수를 생성하고 0으로 초기화  
2) 각각의 사용자가 방문할때마다 실행되는 Session_Start 이벤트에서는 이 CurrentVisit 변수의 값을 1씩 증가시켜 현재 접속자 수를 증가시킴  
3) Session_End 이벤트에서는 각각의 사용자가 나간 후 카운트를 1씩 감소시킴  
4) 최종적으로 Application_End 이벤트에서 카운트 변수를 소멸시킴  
    
<b> Global.asax </b>  
```
using System;
namespace DevCounter
{
    public class Global : System.Web.HttpApplication
    {
        protected void Application_Start(object sender, EventArgs e)
        {
          // [1] 사이트 통계 1/3
          Application["CurrentVisit"] = 0;  // 현재 사용자
        }
        
        protected void Session_Start(object sender, EventArgs e)
        {
            // [2] 사이트 통계 2/3
            Application.Lock();
            Application["CurrentVisit"] = Convert.ToInt32(Application["CurrentVisit"]) + 1;   // 현재 사용자
            Application.UnLock();
        }
        
        protected void Session_End(object sender, EventArgs e)
        {
            // [3] 사이트 통계 3/3
            Application.Lock();
            Application["CurrentVisit"] = (int) Application["CurrentVisit"] -1; // 현재 사용자
            Application.UnLock();        
        }
        
        protected void Application_End(object sender, EventsArgs e)
        {
            // Empty
        }
    }    
}
```   
     
<b> FrmCounter.aspx </b>  
```aspx    
<body>
  <form id="form1" runat="server">
      <div>
          현재 : <asp:Label ID="lblNow" runat="server"> </asp:Label> <br/ >
      </div>
  </form>
</body>
```   
    
<b> FrmCounter.aspx.cs </b>  
```cs
using System;

namespace DevCounter
{
    public partial class FrmCounter : System.Web.UI.Page 
    {
        protected void Page_Load(object sender, EvetArgs e)
        {
            // 현재 접속자 수 표시
            lblNow.Text = Application["CurrentVisit"].ToString();
        }
    }
}
```   
       
- - -  
   
[참고(ASP.NET & Core를 다루는 기술 )](https://book.naver.com/bookdb/book_detail.nhn?bid=11184768)    
     
     
     
