---
layout: post
title:  "DataBinder.Eval Method"
date:   2018-11-30
author: EunHye Jung
categories: .net,cSharp
comment : true
tags: server network http
cover:  "/assets/instacode.png"
---  

### DataBinder.Eval Method   
   

Repeater나 DataList, DataGrid와 같은 컨트롤은 데이터 바인딩에 템플릿(template)을 사용한다.  
이때 실제 데이터 소스와 연결된 것은 아이템을 구성하는 템플릿이 아니라 이를 포함하고 있는 부모 객체 이므로,  
템플릿 내에서는 부모 객체의 데이터 소스에 접근하기 위해서 `Container.DataItem("필드이름")`과 같은 형태로 접근해야 한다.  
바인딩할 아이템을 지정하기 위해 <b>DataBinder.Eval()</b> 메소드를 이용한다.  
  
<i>ex : <%# DataBinder.Eval(Container.DataItem, "CategoryName") %> </i>  
       
<b>Event(Object, String)</b> : 런타임에 데이터 바인딩 식을 계산.  
<b>Event(Object, String, String)</b> : 런타임에 데이터 바인딩 식을 계산하고 결과를 문자열 형식으로 지정.   
      
- - -      
    
#### Example   
   
```C# 
public class Product  
{
    public int ProductID { get; set; }
    public string Name { get; set; }
    public double Price { get; set; }
}    
   
   
public partial class ShowProduct : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        var products = new List<Product>();
        products.Add(new Product() { ProductID = 1, Name = "Bike", Price = 150.00 });
        products.Add(new Product() { ProductID = 2, Name = "Helmet", Price = 19.00 });
        products.Add(new Product() { ProductID = 3, Name = "Tire", Price = 10.00 });
        
        ProductList.DataSource = products;
        ProductList.DataBind();
    }
}
```   
  
```ASP.NET  
<asp:Repeater ID = "ProductList" runat="server">
    <ItemTemplate>
        <%# Eval("Name") %> for only <%# Eval("Price", "{0:c}") %>
        <br />
        <a href = '<%# Eval("ProductID", "details.asp?id={0}") %'> See Details </a>  
        <br />
        <br />
    </ItemTemplate>
</asp:Repeater>
```
     
- - -  
    
[참고사이트(https://docs.microsoft.com/ko-kr/dotnet/api/system.web.ui.databinder.eval?view=netframework-4.7.2)](https://docs.microsoft.com/ko-kr/dotnet/api/system.web.ui.databinder.eval?view=netframework-4.7.2)   
[참고사이트(http://www.hoons.net/lecture/view/24)](http://www.hoons.net/lecture/view/24)  
  
