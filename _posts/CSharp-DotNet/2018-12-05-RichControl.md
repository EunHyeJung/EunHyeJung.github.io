---
layout: post
title:  "ASP.NET Rich Control"
date:   2018-12-05
author: EunHye Jung
categories: csharp,dotnet
comment : true
tags: csharp dotnet asp.net richcontrol
cover:  "/assets/instacode.png"
---  
   
## <font color = "#0E4D92"> Rich Control </font>    
     
     
- - -   
     
     
### <font color="#04635b"> FileUpload 컨트롤 </font>   
    
파일업로드 컨트롤은 로컬 컴퓨터에 있는 데이터(파일)을 원격 서버에 올리고자 할 때 파일을 첨부해준다.  
   
<b> 주요 명령어 </b>  
* FileUpload.HasFile : 파일이 첨부되었는지 확인  
* FileUpload.SaveAs() : 서버 측 경로에 파일 저장  
* FileUpload.PostedFile.ContentLength : 첨부된 파일의 사이즈(Byte)   
       
 <b> FrmFileUpload.aspx </b>    
 ```aspx
<body>
	<form id="form1" runat="server">
		<div>
			<asp:FileUpload ID="ctlFileUpload" runat="server" />
			<br />
			<asp:LinkButton ID="btnUpload" runat="server" OnClick="btnUpload_Click"> 파일업로드 </asp:LinkButton>
			<br />
			<asp:Label ID="lblResult" runat="server"> </asp:Label>
		</div>
	</form>
</body>
```    
    
<b> FrmFileUpload.aspx.cs </b>   
```cs
public partial class FrmFileUpload : System.Web.UI.Page
{
	protected void Page_Load(object sender, EventArgs e)
	{
		// Empty
	}
	protected void btnUpload_Click(object sender, EventArgs e)
	{
		// [1] 파일이 첨부되었다면
		if (ctlFileUpload.HasFile)
		{
			// [2] App_Data 폴더로 파일 업로드
			ctlFileUpload.SaveAs(Server.MapPath(".") + "\\\files\\" + ctlFileUpload.FileName);
			// [3] 다운로드 링크 만들기
			lblResult.Text = String.Format("<a href='{0}{1}'> {1} </a>", "./files/",Server.UrlEncode(ctlFileUpload.FileName));
		}
	}
}
```  
     
     
- - -   
     
     
### <font color="#04635b"> MultiView 컨트롤과 View 컨트롤 </font>   
   
멀티뷰 컨트롤과 뷰 컨트롤은 일반적으로 같이 사용된다.  
뷰 컨트롤은 각각의 모양을 정의하고, 멀티뷰 컨트롤은 여러 모양으로 정의된 뷰 컨트롤 중에서 하나를 출력하는 컨테이너 역할을 한다.  
두 컨트롤을 사용하면 지정된 공간에 여러가지 내용을 동작으로 출력 가능하다.  
      
<b> FrmMultiView.aspx </b>   
```aspx  
<body>
	<form id="form1" runat="server">
		<div>
			<asp:MultiView ID="ctlMultiView1" runat="server">
				<asp:View ID="ctlView1" runat="server">
					<asp:Button ID="btnLogin" runat="server" Text="로그인" OnClick="btnLogin_Click" />
				</asp:View>
				<asp:View Id="ctlView2" runat="server">
					<asp:Button ID="btnLogout" runat="server" Text="로그아웃" OnClick="btnLogout_Click" />
				</asp:View>
			</asp:MultiView>
		</div>
	</form>
</body>
```    
   
<b> FrmMultiView.aspx.cs </b>    
```cs     
public partial class FrmMultiView : System.Web.UI.Page
{
	protected void Page_Load(object sender, EventArgs e)
	{
		if(!isPostBack)
		{
			// [1] 첫번째(인덱스 : 0) 뷰 컨트롤 활성화
			ctlMultiView1.ActiveViewIndex = 0;
		}
	}
	protected void btnLogin_Click(object sender, EventArgs e)
	{
		// [2] 두번째 뷰 컨트롤 활성화
		this.ctlMultiView1.ActiveViewIndex = 1;
	}
	protected void btnLogout_Click(object sender, EventArgs e)
	{
		// [3] 첫번째 뷰 컨트롤 활성화
		this.ctlMultiView1.ActiveViewIndex = 0;
	}
}
```    
     
     
- - -   
     
     
### <font color="#04635b"> Panel 컨트롤 </font>         
     
패널 컨트롤은 HTML의 div 태그와 같이 HTML 및 웹 폼 구성요소를 담는 컨테이너 역할을 하는 컨트롤이다.  
    
* ASP.NET의 소스 부분 : `<asp:Panel>`     
* 웹 브라우저의 출력 부분 : `<div>`   
    
<b> Panel 컨트롤을 사용해 그룹으로 보이기 및 숨기기</b>  
<b> FrmPanel.apsx </b>  
```aspx  
<body>
<form id="form1" runat="server">
  <div>
    <asp:Panel ID="pnlFirst" runat="server" Height="50px" Width="200px" ScrollBars="Vertical">
      Hello <br/>
      Hello <br/>
      Hello <br/>
    </asp:Panel>
    
    <asp:Panel ID="pnlSecond" runat="server" Heigth="50px" Width="200px" GroupingText="그룹 상자">
      Nice to meet you <br />
    </asp:Panel>
    <br />
    <hr />
    
    <asp:Panel ID="pnlCommand" runat="server" Height="50px" Width="360px" DefaultButton="btnShowPanel2">
        <asp:Button ID="btnShowPanel1" runat="server" Text="첫번째 패널 보이기" OnClick="btnShowPanel1_Click" />
        <asp:Button ID="btnShowPanel2" runat="server" Text="두번째 패널 보이기" OnClick="btnShowPanel2_Click" />
        <br />
        <asp:TextBox ID="txtMessage" runat="server" Width="344px"> 여기에서 엔터를 누르면 버튼이 클릭됨 </asp:TextBox>
    </asp:Panel>
  </div>
</form>
</body>
```   
   
<b> FrmPanel.aspx.cs </b>  
```cs  
public partial class FrmPanel : System.Web.UI.Page
{
	protected void Page_Load(object sender, EventArgs e)
	{
		if(!IsPostBack)
		{
			// 텍스트박스에 포커스 두기
			Page.SetFocus(txtMessage)
		}
		// 로드될 첫번째 패널만 보이기
		this.pnlFirst.Visible = true;
		this.pnlSecond.Visible = false;
		// 첫번째 패널 -> 두번째 버튼 보이기
		btnShowPanel1.Visible = false;
		btnShowPanel2.Visible = true;
	}
	protected void btnShowPanel1_Click(object sender, EventArgs e)
	{
		this.pnlFirst.Visible = true;
		this.pnlSecond.Visible = false;	
		btnShowPanel1.Visible = false;
		btnShowPanel2.Visible = true;
		// 텍스트박스에 포커스
		SetFocus(txtMessage);
		pnlCommand.DefaultButton = "btnShowPanel2";
	}
	protected void btnShowPanel2_Click(object sender, EventArgs e)
	{
		this.pnlFirst.Visible = false;
		this.pnlSecond.Visible = true;
		btnShowPanel1.Visible = true;
		btnShowpanel2.Visible = false;
		// 텍스트 박스에 포커스
		SetFocus(txtMessage);
		pnlCommand.DefaultButton = "btnShowPanel1";
	}
}  
```  
     
     
- - -   
     
     
### <font color="#04635b"> PlaceHolder 컨트롤 </font>        
   
플레이스홀더(틀) 컨트롤은 패널 컨트롤과 비슷한 역할을 하나 특정한 태그로 묶이지 않는것이 특징이다.  
     
<b> PlaceHolder 컨트롤에 동적으로 버튼 컨트롤 추가하기 </b>  
<b> FrmPlaceHolder.aspx</b>    
```aspx  
<form id="form1" runat="server">
  <div>
	<asp:PlaceHolder ID="ctlPlaceHolder" runat="server"> </asp:PlaceHolder>  
	<hr />
	<asp:Label ID="lblDisplay" runat="server"> </asp:Label>
  </div>
</form>
```  
   
<b> FrmPlaceholder.aspx.cs </b>  
```cs  
public partial class FrmPlaceHolder : System.Web.UI.Page
{
	protected void Page_Load(object sender, EventArgs e)
	{
		// [1] 버튼 개체 하나 생성
		Button btn1 = new Button();
		btn1.ID = "btn1";
		btn1.Text = "버튼1";
		btn1.Click += btn_Click;
		// [2] PlaceHolder에 버튼 추가
		ctlPlaceHolder.Controls.Add(btn1);
		Literal ltr = new Literal();
		ltr.Text="<br />";
		ctlPlaceHolder.Controls.Add(ltr);
		
		Button btn2 = new Button();
		btn2.ID = "btn2";
		btn2.Text = "버튼2";
		btn2.Click += btn_Click;
		ctlPlaceHolder.Controls.Add(btn2);
	}
	private void btn_Click(object sender, EventArgs e)
	{
		lblDisplay.Text = (sender as Button).Text + "버튼이 클릭됨. <br />";
		Button btnCurrent = sender as Button;
		lblDisplay.Text = btnCurrent.ID + "버튼입니다.<br />";
		// 부모 컨트롤(컨테이너)로부터 자식컨트롤을 읽어오는 코드
		lblDisplay.Text += ((Button) ctlPlaceHolder.FindControl(btnCurrent.ID)).Text + "버튼 ?";
	}	
}
```  
     
- - -  
   
[참고(ASP.NET & Core를 다루는 기술 )](https://book.naver.com/bookdb/book_detail.nhn?bid=11184768)    
     
     
     
