---
layout: post
title:  "ASP.NET HTML 대체 컨트롤 (1)"
date:   2018-12-03
author: EunHye Jung
categories: csharp,dotnet
comment : true
tags: csharp dotnet asp.net
cover:  "/assets/instacode.png"
---  
   
## <font color = "#0E4D92"> HTML 대체 컨트롤 </font>    
   
ASP.NET에서 제공하는 표준 컨트롤 중에는 하이퍼링크, 이미지, 테이블 등 기존에 HTML 태그로 표현하던 (정적으로) 내용을 서버 컨트롤을 사용해 선언적 및 동적으로 HTML 태그를 만들어 내는 컨트롤 등을 제공한다.  
     
     
- - -   
     
     
### <font color="#04635b"> DropDownList 컨트롤 </font>   
    
<b> FrmDropDownList.aspx </b>   
```aspx   
<body>
  <form id="form1" runat="server">
    <div>
      <asp:DropDownList ID="lstJob" runat="server" AutoPostBack="true" OnSelectedIndexChanged="lstJob_SelectedIndexChanged">
      <asp:ListItem> 회사원 </asp:ListItem>
      <asp:ListItem> 공무원 </asp:ListItem>
      <asp:ListItem Selected="True"> 개발자 </asp:ListItem>
      </asp:DropDownList>
      <hr />
      <asp:Label ID="lblDisplay" runat="server" />
    </div>
  </form>
</body>
```  
   
<b> FrMDropDownList.aspx.cs </b>  
```cs   
using System;

namespace DevStandardControl
{
    public partial class FrmDropDownList : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!Page.IsPostBack && lstJob.Items.Count > 1)
            {
                this.lstJob.SelectedIndex = 1;
            }
        }
        
        protected void lstJob_SelectedIndexChanged(object sender, EventArgs e)
        {
            // 문자열 변수 선언과 동시 초기화
            string strMsg = String.Empty;
            strMsg = lstJob.SelectedItem.Text + "을(를) 선택하였습니다.";
            
            // 레이블에 현재 선택된 값 출력
            this.lblDisplay.Text = strMsg;
        }
    }
}
```  

   
- - -  
   
   
### <font color="#04635b"> ListBox 컨트롤 </font>   
   
<b>FrmListBox.aspx</b>  
```aspx  
<body>
  <form id="form1" runat="server">
    <div>
      <asp:ListBox ID="lstHobby" runat="server" SelectionMode="Multiple"> </asp:ListBox>
      <hr />
      <asp:Button ID="btnPrint" runat="server" Text="선택한 값 출력" OnClick="btnPrint_Click"/>
      <hr />
      <asp:Label ID="lblDisplay" runat="server"> </asp:Label>
    </div>
   </form>
</body>
```  
   
<b>FrmListBox.aspx.cs</b>  
```cs
using System;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace DevStandardControl
{
  public partial class FrmListBox : System.Web.UI.Page
  {
      protected void Page_Load(object sender, EventArgs e)
      {
          // 처음 로드할 때만 항목 추가
          if (!Page.IsPostBack)
          {
              // 동적으로 항목 추가
              this.lstHobby.Item.Add("축구");
              this.lstHobby.Item.Add("농구");
              
              // ListItem 클래스
              ListItem li = new ListItem();
              li.Text = "배구";
              li.Value = "Volleyball";
              lstHobby.Items.Add(li);
          }
      }
  }
}
```
    

- - -  
   
   
### <font color="#04635b"> CheckBox 컨트롤 </font>   
   
체크박스 컨트롤은 HTML의 <input type="CheckBox">와 같은 체크박스를 만든다.  
    
<b> FrmCheckBox.aspx </b>  
```aspx 
<body>
    <form id="form1" runat="server">
        <div>
            <asp:CheckBox ID="chkCSharp" runat="server" Text="C#" />
            <br />
            <asp:CheckBox ID="chkAspNet" runat="server" Text="ASP.NET" />
            <hr />
            <asp:Button ID="btnCheck" runat="server" Text="확인" OnClick="btnCheck_Click" />
            <hr />
            <asp:Label ID="lblDisplay" runat="server"> </asp:Label>
        </div>
    </form>
</body>
```   
    
<b> FrmCheckBox.aspx.cs </b>  
```cs   
using System;

namespace DevStandardControl
{
  public partial class FrmCheckBox : System.Web.UI.Page
  {
      protected void Page_Load(object sender, EventArgs e)
      {
          // Empty
      }
      
      protected void btnCheck_Click(object sender, EventArgs e)
      {
          string strMsg = "선택한 값 : <br />";
          if (this.chkCSharp.Checked)
          {
              strMsg += chkCSharp.Text + "<br />";
          }
          if (this.chkAspNet.Checked)
          {
              strMsg += chkAspNet.Text + "<br />";
          }
          lblDisplay.Text = strMsg;
      }
  }
}
```    
    

- - -  
   
   
### <font color="#04635b"> CheckBoxList 컨트롤 </font>   
    
체크박스 리스트 컨트롤은 같은 주제에 대해서 여러 항목을 선택하고자 할 때 사용.   
   
<b> FrmCheckBoxList.aspx </b>  
```aspx  
<body>
    <form id="form1" runat="server">
        <div>
            <asp:CheckBoxList ID="lstHobby" runat="server" RepeatDirection="Horizontal" RepeatLayout="Flow" RepeatColumns="2">
                <asp:ListItem Selected="True"> 축구 </asp:ListItem>
                <asp:ListItem> 농구 </asp:ListItem>
                <asp:ListItem> 배구 </asp:ListItem>
            </asp:CheckBoxList>
            <hr />
            <asp:LinkButton ID="btnOK" runat="server" OnClick="btnOK_Click"> 확인 </asp:LinkButton>
            <hr />
            <asp:Label ID="lblDisplay" runat="server"> </asp:Label>
        </div>
    </form>
</body>
```
    
<b> FrmCheckBoxList.aspx.cs</b>   
```cs
using System;

namespace DevStandardControl
{
    public partial class FrmCheckBoxList : System.Web.UI.Page
    {
        protected void Page_Loda(object sender, EventArgs e)
        {
            // Empty;
        }
        
        protected void btnOK_Click(object sender, EventArgs e)
        {
            string strMsg = "선택한 취미는 <br />";
            for (int i = 0; i < lstHobby.Items.Count; i++)
            {
                if (lstHobby.Items[i].Selected)
                {
                    strMsg += lstHobby.Items[i].Text + "<br />";
                }
            }
            lblDisplay.Text = strMsg;
        }
    }
}
```   
     

- - -  
   
   
### <font color="#04635b"> 단일, 다중 항목 가져오기 </font>   
    
<b> FrmInputControl.aspx </b>  
```aspx
<body>
    <form id="form1" runat="server">
		<table style="width : 500px">
			<tr>
					<td style="width : 200px"> 체크박스(이용약관) : </td>
					<td style="width : 100px"> 
							<asp:CheckBox ID="chkAgree" runat="server" Text="동의" Checked="true" Width="122px" />
					</td>
			</tr>
			<tr>
					<td style="width : 200px"> 체크박스 리스트(취미) : </td>
					<td style="width : 100px">
							<asp:CheckBoxList ID="lstHobby" runat="server" RepeatColumns="2" RepeatDirection="Horizontal" RepeatLayout="Flow" Width="202px">
								<asp:ListItem Selected="True" Value="S"> 축구 </asp:ListItem>
								<asp:ListItem Value="V"> 배구 </asp:ListItem>
								<asp:ListItem Selected="True" Value="B"> 농구 </asp:ListItem>
							</asp:CheckBoxList>
					</td>
			</tr>
			<tr>
					<td style="width : 200px"> 라디오 버튼(성별) : </td>
					<td style="width : 100px">	
							<asp:RadioButton ID="rdoMan" runat="server" Text="남자" GroupName="Gender" Checked="true" />
							<asp:RadioButton ID="rdoWomen" runat="server" Text="여자" GroupName="Gender" />
					</td> 
			</tr>
			<tr>
					<td style="width : 200px; height : 24px"> 드롭다운 리스트(단일선택) </td>
					<td style="width : 100px; heigth : 25px">
						<asp:DropDownList ID="lstJob" runat="server">
							<asp:ListItem> 회사원 </asp:ListItem>
							<asp:ListItem Selected="True"> 공무원 </asp:ListItem>
							<asp:ListItem> 무직 </asp:ListItem>
						</asp:DropDownList>
					</td>
			</tr>
			<tr>
					<td style="width : 200px"> 리스트박스(다중 선택) </td>
					<td style="width : 100px"> 
						<asp:ListBox ID="lstFavorite" runat="server" SelectionMode="Multiple"> </asp:ListBox>
					</td>
			</tr>
		</table>
		<br /> <br />
		<asp:Button ID="btonOK" runat="server" Text="확인" OnClick="btnOk_Click" /> <br />
		<asp:Label ID="lblDisplay" runat="server" />
    </form>
</body>
````
   
<b> FrmInputControl.aspx.cs </b> 
```
using System;
using System.Text;
using System.Web.UI;
using System.Web.UI.Web.Controls;
namespace DevStandardControl
{
	public partial class FrmInputControl : System.Web.UI.Page
	{
		protected void Page_Load(object sender, EventArgs e)
		{
			// Page.IsPostBack : 처음 로드하면 false, 포스트백(다시 게시)되면 true
			if (!Page.IsPostBack)
			{
				BindFavorite();
			}
		}
		
		private void BindFavorite()
		{
			// 동적으로 ListItem을 채우는 3가지 방법
			lstFavorite.Items.Add("C#");
			this.lstFavorite.Items.Add("ASP.NET");
			ListItem li = new ListItem();
			li.Text = "JavaScript";
			li.Value = "TypeScript";
			this.lstFavorite.Items.Add(li);
			ListItem listItem = new ListItem("닷넷", ".NET");
			this.lstFavorite.Items.Add(lstItem);
		}		
		protected void BtnOk_Click(object sender, EventArgs e)
		{
			StringBuilder sb = new StringBuilder();
		
			// [1] 체크박스의 내용 가져오기 : 단일값
			if (this.chkAgree.Checked)
			{
				sb.Append("[1]" + this.chkAgree.Text + "<br />");
			}
			// [2] 체크박스 리스트의 내용 가져오기 : 다중값
			if (this.lstHobby.Items[0].Selected) // 0번째 항목이 선택되었다면
			{
				sb.Append("[2]" + this.lstHobby.Items[0].Value + "<br />");
			}
			if (this.lstHobby.Items[1].Selected)
			{
				sb.AppendFormat("[2] {0} <br />", this.lstHobby.Items[1].Value);
			}
			if (this.lstHobby.Items[2].Selected)
			{
				sb.AppendFormat("[2] {0} <br />", this.lstHobby.Items[2].Value);
			}
			// [3] 라디오버튼 값 가져오기 : 단일값
			if (this.rdoMan.Checked)
			{
				sb.AppendFormat("[3] {0} 선택 <br />", rdoMan.Text);
			}
			else
			{
				sb.AppendFormat("[3] {0} 선택 <br />", rdoWomen.Text);
			}
			// [4] 드롭다운리스트 값 받아오기 : 단일값
			sb.AppendFormat("[4] {0} <br />", lstJob.Items[lstJob.SelectedIndex].Value);
			// [5] 리스트박스 : 다중값
			for (int i = 0; i < lstFavorite.Items.Count; i++)
			{	
				if (lstFavorite.Items[i].Selected)
				{
					sb.AppendFormat("[6] {0} <br />", lstFavorite.Items[i].Value);
				}
			}
			// [!] 출력
			this.lblDisplay.Text = sb.ToString();
		}
	}
}
```    
   
   
- - -  
   
[참고(ASP.NET & Core를 다루는 기술 )](https://book.naver.com/bookdb/book_detail.nhn?bid=11184768)    
     
