---
layout: post
title:  "XmlDocument-XML쓰기"
date:   2018-12-19
author: EunHye Jung
categories: csharp,dotnet
comment : true
tags: csharp dotnet asp.net xml
cover:  "/assets/instacode.png"
---  
   
## <font color = "#0E4D92"> XmlDocument </font>       
   
XmlDocument를 사용하여 XML데이터를 쓰기 위해서는 먼저 XmlDocument 객체를 생성하고, 이 객체에 루트 노드를 추가하고 다시 루트노드 밑에 필요한 자식들을 추가해 나간다.  
   
XML Element를 생성하기 위해서는 XmlDocument의 `CreateElement()` 메서드를 사용하고, Attribute를 생성하기 위해서는 XmlDocument의 `CreateAttribute()` 메서드를 사용한다.  
생성된 Element는 XmlNode 클래스 객체가 되는데, `AppendChild()` 메서드를 통해 부모 노드에 추가시키면 된다.  
CreateAttributes() 메서드로 생성된 Attribute는 XmlAttribute 클래스 객체가 되는데, 이는 Element 객체의 `Attributes.Append()`를 통해 Attribute를 추가하게 된다.  
   
XmlDocument 내에 모든 노드들이 생성되고 자식노드로 추가되었으면, `Save()` 메서드를 호출하여 XML 파일에 저장하면 된다.    
   
           
#### <font color="#04635b"> Employee 데이터를 XML로 생성하는 예제 </font>  
   
```
// using System.Xml;

XmlDocument xdoc = new XmlDocument();

// root node
XmlNode root = xdoc.CreateElement("Employees");
xdoc.AppendChild(root);

// Employee #1001
XmlNode emp1 = xdoc.CreateElement("Employee");
XmlAttribute attr = xdoc.CreateAttribute("Id");
attr.Value = "1001";
emp1.Attributes.Append(attr);

XmlNode name1 = xdoc.CreateElement("Name");
name1.InnerText = "Tim";
emp1.AppendChild(name1);

XmlNode dept1 = xdoc.CreateElement("Dept");
dept1.InnerText = "Sales";
emp1.AppendChild(dept1);

root.AppendChild(emp1);

// Employee #1002
var emp2 = xdoc.CreateElement("Employee");
var attr2 = xdoc.CreateAttribute("Id");
attr2.Value = "1002";
emp2.Attributes.Append(attr2);

var name2 = xdoc.CreateElement("Name");
name2.InnerText = "John";
emp2.AppendChild(name2);

XmlNode dept2 = xdoc.CreateElement("Dept");
dept2.InnerText = "HR";
emp2.AppendChild(dept2);

root.AppendChild(emp2);

// XML 파일 저장
xdoc.Save("파일 저장 경로");
```   
      
     
c) CDATA 섹션(`<! [CDATA[]]>`)은 구문 분석기가 마크업이 아닌 문자데이터로만 해석되도록 한다.   
    
- - -  
   
[출저(예제로배우는 C#프로그래밍)](http://www.csharpstudy.com/data/Xml-xmldoc.aspx)
   
