---
layout: post
title:  "ASP.NET HTML 대체 컨트롤 (2)"
date:   2018-12-04
author: EunHye Jung
categories: csharp,dotnet
comment : true
tags: csharp dotnet asp.net
cover:  "/assets/instacode.png"
---  
   
## <font color = "#0E4D92"> HTML 대체 컨트롤 </font>    
   
ASP.NET에서 제공하는 표준 컨트롤 중에는 하이퍼링크, 이미지, 테이블 등 기존에 HTML 태그로 표현하던 (정적으로) 내용을 서버 컨트롤을 사용해 선언적 및 동적으로 HTML 태그를 만들어 내는 컨트롤 등을 제공한다.  
     
     
- - -   
     
     
### <font color="#04635b"> HiddenField 컨트롤 </font>   
   
게시물의 글 번호나 페이지번호 등 굳이 웹 폼에 보일 필요가 없는 내용에는 히든 필드를 사용한다.  
   
속성  
* Value : 히든필드에 임시로 저장한 값  
* Visible : 히든필드 컨트롤을 <input type="hidden" />으로 표현할지 결정  
이벤트   
* ValueChanged : 히든필드의 값이 변경될 때 발생   
     
<b> FrmHiddenField.aspx </b>  
```aspx
<body>
    <form id="form1" runat="server">
		<asp:HiddenField ID="ctlHidden" runat="server" />
		<asp:Button ID = "btnOK" runat="server" OnClick="BtnOK_Click" Text="히든필드에 저장된 값 출력" />
	</form>
</body>
```   
      
<b> FrmHiddenField.aspx.cs </b>   
```cs  
using System;
using System.Text;
using System.Web.UI;
using System.Web.UI.Web.Controls;
namespace DevStandardControl
{
	public partial class FrmHiddenField : System.Web.UI.Page
	{
		protected void Page_Load(object sender, EventArgs e)
		{
			if(!Page.IsPostBack)
			{
				this.ctlHidden.Value = DateTime.Now.ToShortTimeString();
			}
		}
		protected void BtnOK_Click(object sender, EventArgs e)
		{
			// 히든필드에 저장된 문자열 출력
			Response.Write(ctlHidden.Value);
		}
	}
}
```   
     
     
- - -   
     
     
### <font color="#04635b"> Literal 컨트롤 </font>   
   
리터럴 컨트롤은 정적 텍스트(Static Text)를 페이지에 출력하는 컨트롤  
<span> 태그를 생성하는 Label 컨트롤과 달리, 일반 텍스트만 출력하므로 조금더 깔끔한 HTML 소스표현이 가능하다.  
   
<b> FrmLiteral.aspx </b>   
```aspx  		현재 날짜 : 
		<asp:Literal ID="ctlDate" runat="server"> </asp:Literal> <br />
        현재 시간 : 
		<asp:Literal ID="lblTime" runat="server"> <asp:Literal> <br />
```  
<b> FrmLiteral.aspx.cs </b>  
```cs
	public partial class FrmLiteral: System.Web.UI.Page
	{
		protected void Page_Load(object sender, EventArgs e)
		{
			// 리터럴에 날짜 출력
			ctlDate.Text = DateTime.Now.ToShortDateString();
			// 테이블에 시간 출력
			lblTime.Text = DateTime.Now.ToShortTimeString();
		}
	}
```   
    
