---
layout: post
title:  "빅데이터 관련 기술, 기초 용어"
date:   2018-06-09
author: EunHye Jung
categories: etc
tags:	bigdata
cover:  "/assets/instacode.png"
---
   
### 빅데이터를 다루는 플랫폼 기술  
   
여러 플랫폼을 `저장 시스템`, `처리 방식`, `분석 방식`이라는 세가지 측면으로 나눠볼 수 있다.   
  
* 저장 시스템     
  병렬 DBMS와 NoSQL은 모두 대량의 데이터를 저장하기 위해 `수평 확장 접근 방식`을 취하고 있다는 점에서는 동일하다.  
  SAN(Storage Area Network), NAS(Network Attached Storage)  
  클라우드 파일 저장 시스템, GFS(Google File System), HDFS(Hadoop Distributed File System)    
   
* 처리 방식  
  병렬 처리의 핵심은 `분할 점령(Divide and Conquer)`이다.  
  즉, 데이터를 독립된 형태로 분할하고, 이를 병렬적으로 처리하는것.  
  빅데이터에서 데이터 처리란 이렇게 문제를 여러 개의 작은 연산으로 나누고, 이를 취합해서 하나의 결과로 만드는것을 말한다.  
  물론, 연산 의존성이 있는 경우 병렬 연산의 이점을 살릴 수 없기에, 이러한 점을 고려한 데이터 저장과  처리가 필요.  
    
* 분석 방식  
  데이터에서 의미를 찾는 과정을 `KDD(Knowledge Discovery in Database)라고 한다.  
  관심있는 데이터의 일부 또는 전부를 처리/분석해서 추이나 의미있는 값을 추출하거나 지금까지 미처 알지 못했던 사실을 발견해서 이를 지식으로 만드는 것이다.      
  이를 위하여 인공지능, 기계 학습, 통계, 데이터베이스 등 여러 분야의 기술을 종합적으로 적용하고 있다.  

- - -

### Apache Hadoop  
  
* 대용량 데이터를 분산처리할 수 있는 자바기반의 오픈소스 프레임워크.  
* GFS(Google File System)와 맵리듀스(MapReduce)를 구현한 결과물.  
* Hadoop의 핵심은 `HDFS(Hadoop Distributed File System)`와 `MapReduce 프레임워크`다.      
  분산 파일 시스템 형태로 용량을 확장할 수 있는 파일 시스템인 HDFS에 데이터를 저장하고,  
  이렇게 저장된 데이터를 바탕으로 MapReduce연산을 실행해 원하는 데이터를 얻을 수 있다.  
   
### Apache Sqoop   
   
* 관계형 DB와 같은 구조화된 데이터저장소들과 아파치 하둡 사이에서 많은 양의 데이터를 효율적으로 전송하기 위해 고안된 툴.  

### Impala   
  
* HDFS에 저장되어 있는 데이터를 SQL를 이용해서 실시간으로 분석할 수 있는 시스템. 
* MapReduce 프레임워크를 이용하지 않고, 분산 질의 엔진을 이용해 분석하기 때문에 빠른 결과를 제공할 수 있음.  
* Impala와 Hive의 차이는 실시간성 여부이다.  
  Hive는 데이터 접근을 위해 MapReduce 프레임워크를 이용하는 반면에,  
  Impala는 응답시간을 최소한으로 줄이기 위해, 고유의 분산 질의 엔진을 사용한다. 이 분산 질의 엔진은 클러스터 내 모든 데이터 노드에 설치되도록 했다.   

### Spark   
* 하둡기반 실시간 빅데이터 분석 플랫폼.    
* 하둡과 유사한 형태로 작동, 메모리에 캐시된 데이터를 사용하여 분석.  
  디스크에 접근하는 비용을 줄임으로써 40배이상 속도 향상.  
  
  
  
  
[참조(빅데이터를 위한 플랫폼들)](https://d2.naver.com/helloworld/29533) 
[참조(Hadoop에서의 실시간 SQL 질의: Impala)](https://d2.naver.com/helloworld/246342)
[참조(클라우데라)](https://www.cloudera.com/)
