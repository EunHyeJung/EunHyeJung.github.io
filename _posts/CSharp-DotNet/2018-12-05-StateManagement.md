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
      
        
### <font color="#04635b"> Global.asax 파일  </font>  
    
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
      
        
### <font color="#04635b"> 캐싱(Caching)  </font>   
  
ASP.NET에서는 자주 변경되지 않는 페이지에 대한 내용을 서버 측 캐시에 저장하고 있다가 클라이언트의 요청이 들어오면 바로 출력시켜준다.   
웹 폼에 캐싱 기능을 적용할 때는 선언형으로 적용하는 방법과 코드 기반으로 적용하는 방법 두가지가 있다.   
    
    
<b> 선언적 구현 </b>  
<b> FrmCachingWebUserControl.ascx </b>  
```aspx
<%@ Control Language="C#" AutoEventWireup="true" CodeBehind="FrmCachingWebUserControl.ascx.cs" Inherits="DevCaching.FrmCachingWebUserControl" %>


<%@ OutputCache Duration="5" VaryByParam="None" %>

현재 시간(웹 폼 사용자 정의 컨트롤):
<asp:Label ID="lblTimeWebUserControl" runat="server" Text="Label"> </asp:Label>
```    
    
<b> FrmCachingWebUserControl.ascx.cs </b>  
```cs
using System;

namespace DevCaching
{
    public partial class FrmCachingWebUserControl : System.Web.UI.UserControl
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // 현재 시간 출력 : 5초에 한번씩 출력
            lblTimeWebUserControl.Text = DateTime.Now.ToString();
        }
    }
}
```   
   
<b> FrmCaching.aspx </b>    
```aspx   
<%@ Register Src="~/FrmCachingWebUserControl.ascx" TagPrefix="uc1" TagName="FrmCachingWebUserControl" %>

<body>
<form id="form1" runat="server">
    <div>
        현재 시간 (웹 폼):
        <asp:Label ID="lblTimeWebForms" runat="server" Text="Label"> </asp:Label>
        <hr />
        <uc1:FrmCachingWebUserControl runat="server" ID="FrmCachingWebUserControl" />
    </div>
</form>
</body>
```   
    
<b> FrmCaching.aspx.cs </b>  
```cs   
using System;

namespace DevCaching
{
    public partial calss FrmCaching : System.Web.UI.Page
    {
        protecteod void Page_Load(object sender, EventArgs e)
        {
            // 현재 시간 출력 : 매번 바로 출력
            lblTimeWebForms.Text = DateTime.Now.ToString();
        }
    }
}
```  
        
<b>코드 기반 적용</b>     
<b> FrmCachingResponseCache.aspx.cs </b>   
```cs  
using System;
using System.Web;

namespace DevCaching
{
    public partial class FrmCachingResponseCache : System.Web.UI.Page
    {
          protecteod void Page_Load(object sender, EventArgs e)
          {
              // 코드기반으로 캐싱기능 적용하기
              // 현재날짜 출력
              Response.Write(DateTime.Now.ToString());
              // 캐싱 설정
              Response.Cache.SetCacheability(HttpCacheability.Public);
              // 캐싱 유효기간 설정
              Resposne.Cache.SetExpire(DateTime.Now.AddSeconds(60));
              // 매개 변수 방식 지정
              Response.Cache.VaryByParams["*"] = true;
          }
    }
}
```   

    
     
- - -   
      
        
### <font color="#04635b"> 환경 설정 파일인 Web.config  </font>   
    
Web.config 파일은 웹프로젝트 관련 환경설정 파일이 들어오는 곳이다.  
기본값만 사용해도 상관은 없지만 큰 규모의 앱으로 확장하거나 특정 기능 사용시에는 Web.config 파일을 수정해야 하는 경우가 생긴다.  
크로스 플랫폼 기반의 ASP.NET Core에서는 JSON(JavaScript Object Notation) 기반의 appsetting.json 파일이 Web.config 파일의 기능 대부분을 대체한다.   
     
<b> Web.Config 파일의 정보를 읽어오는 클래스 사용하기 </b>  
Web.cofing 파일에 두가지 섹션 추가  
```
<configuration>
    <appSettings>
        <!-- 프로그램 내에서 사용되는 설정값 저장 -->
        <!-- [1] 사이트 이름 -->
        <add key="SITE_NAME" value="ASP.NET" />
        <add key="COMPANY_NAME" value="회사이름 "/>
    </appSettings>
    
    <connectionStrings>
        <!-- [2] 데이터베이스 연결 문자열 -->
        <add name="ASPNETBOOKTEST_ConnectionString"
            connectionString="server=;database=;uid=;pwd=;"
            providerName="System.Data.SqlClinet"
    </connectionStrings>
    
    <system.web>
    </system.web>
    <system.codedom>
    </system.codedom>
</configuration>
```   
         
<b> FrmConfiguraion.aspx </b>  
```aspx
...
<title> <%= System.Web.Configuration.WebConfigurationManager.AppSettings["SITE_NAME"].ToString() %> </title>
...
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="lblSITE_NAME" runat="server"> </asp:Label>
            <hr />
            <asp:Label ID="lblCOMPNAY_NAME" runat="server"> </asp:Label>
            <hr />
            <asp:Label ID="lblASPNETBOOKTEST_ConnectionString" runat="server"> </asp:Label>
        </div>
    </form>
</body>
```   
     
<b> FrmConfiguration.aspx.cs </b>   
```cs
using System;
using System.Configuration;
using System.Web.Configuration;

. . .  

public partial class FrmConfiguration : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        lblSITE_NAME.Text = WebConfigurationManager.AppSettings["SITE_NAME"].ToString();
        lblCOMPANY_NAME.Text = ConfigurationManager.AppSettings["COMPANY_NAME"].ToString();
        lblASPNETBOOKTEST_ConnectionString.Text = WebConfigurationManager.ConnectionStrings["ASPNETBOOKTEST_ConnectionString"].ConnectionString;
    }
}
```   
     
      
- - -  
   
[참고(ASP.NET & Core를 다루는 기술 )](https://book.naver.com/bookdb/book_detail.nhn?bid=11184768)    
     
     
     
