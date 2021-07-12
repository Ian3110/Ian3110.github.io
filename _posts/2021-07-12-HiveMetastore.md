---
layout: post
title: "하이브 메타스토어(Hive Metastore)"
categories:
- Hive
---

<img src="/assets/img/HiveMetastore.png" width="90%" height="90%" title="HiveMetastore" alt="HiveMetastore"/>
<br/>

## Metastore의 두 가지 메인 기능
---
### 1.	데이터 추상화
* 데이터 추상화 기능은 **데이터 구조**와 **연산**을 효과적으로 사용할 수 있도록 **정리된 수단을 제공**하는 것을 말함.
* 메타 데이터 정보는 **테이블 생성 중 제공**되며 테이블을 참조할 때마다 재사용 됨.
* 이 기능이 없다면 사용자는 쿼리를 작성할 때마다 데이터 형식을 비롯한 여러 정보를 직접 제공해야함.<br/><br/>

### 2.	데이터 검색
* 데이터 검색 기능은 말 그대로 **데이터베이스에 있는 정보 선별 또는 검색**을 의미함.
* 사용자는 데이터 검색을 통해 특정 테이블의 메타 데이터를 참고하여 다른 테이블 스키마를 구축하거나 개선할 수 있음.<br/><br/><br/>

## Hive Metastore의 종류
---
### 1.	내장형 메타스토어 (Embedded Metastore)
* 별도의 데이터베이스를 구축하지 않고 **내장 Dervy DB**를 이용한 모드.
* Hive Server, Metastore Process, Metastore DB가 **동일한 JVM**에서 동작함.
* 한 번에 한 사용자만 접근 가능.<br/><br/>

### 2.	로컬 메타스토어 (Local Metastore)
* Hive Server와 Metastore Process가 동일한 JVM에서 동작함.
* 원격 머신에서 **별도의 프로세스로 실행되는 데이터베이스**와 연결할 수 있음.
* 여러 개의 요청을 한 번에 처리할 수 있음.<br/><br/>

### 3.	원격 메타스토어 (Remote Metastore)
* Hive Server, Metastore Server, Metastore Database가 **다른 JVM**에서 동작함.
* 다른 프로세스가 Metastore 서버와 통신할 때 Thrift 통신을 사용할 수 있음.
* 데이터베이스 계층을 완전히 방화벽으로 차단할 수 있어서 관리 용이성 및 보안이 향상됨.
* 클라이언트는 데이터베이스에 엑세스 하기 위해 더 이상 각 Hive 사용자와 데이터베이스 자격 증명을 공유할 필요가 없음.
