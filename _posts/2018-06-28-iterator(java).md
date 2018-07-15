---
layout: post
title:  "Iterator, ListIterator"
date:   2018-06-28
author: EunHye Jung
categories: java
comment : true
tags:	iterator listIterator collection java
cover:  "/assets/instacode.png"
---
   
[참조](https://www.geeksforgeeks.org/retrieving-elements-from-collection-for-each-iterator-listiterator-enumerationiterator/)
  
   
### For-each    
   For each 반복문은 컬렉션 안에 있는 항목들을 순회하는것을 의미한다!    
     
`  
// for-each를 이용해서 컬렉션 'c'에 있는 원소들 출력
for(Element e : c) {
	System.out.prinln(e);
}
`
  
  Note : 자바8에서는, for-each 반복문을 다음과 같은 람다표현식으로 간단하게 이용할 수 있다.   

`elements.forEach( e -> System.out.println(e));`


- - -

  
### Cursors   
Cursor는 인터페이스다. 그리고 컬렉션에서 데이터들을 하나씩 가지고올때 사용한다.  

   
   * **Iterator Interface**   
     Iterator는 컬렉션을 순회하는 목적으로 사용하는, 컬렉션프레임워크가 제공하는 인터페이스이다.    
     Iterator를 사용하면, 컬렉션에 있는 항목들을 순차적으로 접근할 수 있다.   
     
```
      // Iterator를 사용해서 컬렉션 'c'에 있는 원소들 출력
      for(Iterator i = c.iterator(); i.hasNext(); ) {
      	System.out.println(i.next());
      }
```  
   
       
    Iterator 인터페이스는 3가지 메소드를 가진다.  
    * boolean hasNext() : iterator가 다음에 조회할 원소를 가지고 있으면 true리턴.   
    * element next() : iterator에서 다음 원소를 리턴.  
    * void remove() : 컬렉션에서 iterator에 의해 반환된 가장 마지막 원소를 삭제.   
    
   * **ListIterator Interface**   
     ListInterator도 Iterator와 마찬가지로 컬렉션에서 원소들을 조회하는데 사용되는 인터페이스이다.   
     Iterator와 다른점은 양방향으로 조회가 가능하다.  
     ListIterator는 리스트 기반의 컬렉션을 위한 것이다.   
     
     다음의 메소드가 제공된다.    
     * boolean hasNext() : 리스트에서 정방향으로 다음 원소가 존재한다면, true 리턴.   
     * boolean hasPrevious() : 리스트에서 역방향으로 다음 원소가 존재한다면 ture리턴.  
     * element next() : 리스트에서 다음 원소를 반환하고, 커서(cursor)의 위치를 순반향으로 이동시킴.   
     * element previous() : 리스트에서 이전 원소를 반환하고, 커서(cursor)의 위치를 역방향으로 이동시킴.   
     * void remove() : next()나 previous() 메소드에 의해 반환된 가장 마지막 원소를 리스트에서 삭제.   
     * int nextIndex() : next()를 호출한 후 반환되는 원소의 index값을 리턴.   
     * int previousIndex() : previous()를 호출한 후 반환되는 원소의 indeㅌ값 리턴. (만약, listIterator가 제일 처음에 위치한다면, -1이 리턴됨.)  

   
- - -
    
### 관련문제     
    
[BOJ1406.에디터](https://www.acmicpc.net/problem/1406)    
[BOJ5397.키로커](https://www.acmicpc.net/problem/5397/)   
   
     
