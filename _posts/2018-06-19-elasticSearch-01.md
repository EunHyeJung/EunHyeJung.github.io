---
layout: post
title:  "Elastic Search"
date:   2018-06-19 00:30:00
author: EunHye Jung
categories: etc
tags:	ElasticSearch 엘라스틱서치
cover:  "/assets/instacode.png"
---
   
   
   
# Elastic Search
   
  ElasticSearch는 루씬 기반의 검색엔진, Shay Banon이 시작한 오픈소스 검색서버 프로젝트.  
     
     (https://ko.wikipedia.org/wiki/%EC%9D%BC%EB%9E%98%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98)
      
## Elastic Search의 특징
   
* 실시간 검색 및 분석 서비스 지원  
   

* 분산 및 병렬 처리   
  SPOF(Single Point of Failure) 대응을 위한 높은 가용성 제공
  
* 멀티태넌시   

* 플러그인 형태 구현   
  검색엔진을 직접 수정하지 않고, 필요한 기능에 대한 플러그인을 적용하여 기능확장 가능.


* 기타   
  NoSQL, JSON 기반 문서구조, 버전 충돌 관리 가능, 전문검색(Full Text Search) 지원.
   
   
   
### 기본적으로 사용되는 용어
   
* Index  
  데이터를 저장하기 위한 장소, RDBMS의 데이터베이스와 유사.  
  Index는 하나 또는 여러개의 Document Type을 가질 수 있음.  
       
  cf) Index는 검색에서 포괄적인 의미의 색인, 색인파일이고, Indicie는 elasticsearch내에서 물리적으로 사용되는 색인 또는 색인 파일을 의미.
   
   
* Shard  

  큰 크기의 인덱스를 여러개의 작은 인덱스로 나누어 저장하는 것, 대량의 데이터를 분산처리하기 위한 개념.
  대량의 데이터를 분산처리하여 빠른 결과 처리 가능, 단일 노드에서의 자장소 및 성능에 대한 한계 해결.
   
   - Primary Shard : 색인 시 가장 먼저 생성되는 인덱스, 복제의 기본 소스가됨.
   - Replica Shard : 레플리카 설정에 따라 primary shard를 복제하여 생성된 샤드를 말함.
   
   

* Replica   

  Replica는 서비스 자애시 서비스의 지속성 보장과 검색 처리량을 높이는데 사용.
  Replica는 분산된 다른 노드에 샤드와 같은 데이터를 복제하여, 서비스의 안전성 및 유연성 제공.
   
  기본적으로 primary shard에 색인이 완료되면, 각 노드에 샤드복제가 비동기적(async)으로 이루어짐.
  async 방식으로 복제가 이루어지기 때문에 서비스 진행중 색인작업이 이루어지더라도, 검색 성능 저하를 최소화함.
   
* Document  
  검색에서 가장 기본이 되는 데이터 단위, elasticsearch에 저장되는 하나의 item 혹은 artcle.
  도큐먼트는 RDBMS에서 테이블내 하나의 row에 해당.
   - 도큐먼트의 필드(Field)는 RDBMS에서 테이블의 column에 해당.
  
* Node  
  노드는 elasticsearch를 구성하는 하나의 서버 또는 데몬으로, 독립적으로 동작가능한 서버를 말함.
     
* Cluster  
  클러스터는 하나 이상의 Node(서버)를 데이터 분산을 통해 인덱스/검색 성능을 향상싴리 목적으로 단일 그룹으로 묶는것을 의미.
  



