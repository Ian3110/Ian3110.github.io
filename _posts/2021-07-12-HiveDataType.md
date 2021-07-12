---
layout: post
title: "하이브 데이터형 (Hive Data Type)"
categories:
- Hive
---

하이브 데이터형은 크게 두 가지로 나눌 수 있다. 첫번째는 우리에게 익숙한 원시 데이터형. 이는 자바 데이터형과 같은 방식으로 동작한다. 원시 데이터형에 대해서는 뭐가 있는지 소개정도만 하고 개인적으로 내게 생소했던 timestamp type과 binary type에 대해 자세히 다뤄 보겠다. 두번째는 컬렉션 데이터형이다. 어떤 것인지 궁금하죠? 지금부터 하이브 데이터형에 대해 자세하게 알아봅시다. <br/><br/><br/><br/>


## 원시 데이터형
```
Numeric Types
TINYINT (1-byte signed integer, from -128 to 127)
SMALLINT (2-byte signed integer, from -32,768 to 32,767)
INT/INTEGER (4-byte signed integer, from -2,147,483,648 to 2,147,483,647)
BIGINT (8-byte signed integer, from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807)
FLOAT (4-byte single precision floating point number)
DOUBLE (8-byte double precision floating point number)
DOUBLE PRECISION (alias for DOUBLE, only available starting with Hive 2.2.0)
DECIMAL Introduced in Hive 0.11.0 with a precision of 38 digits
Hive 0.13.0 introduced user-definable precision and scale
NUMERIC (same as DECIMAL, starting with Hive 3.0.0)

Date/Time Types
TIMESTAMP (Note: Only available starting with Hive 0.8.0)
DATE (Note: Only available starting with Hive 0.12.0)
INTERVAL (Note: Only available starting with Hive 1.2.0)

String Types
STRING
VARCHAR (Note: Only available starting with Hive 0.12.0)
CHAR (Note: Only available starting with Hive 0.13.0)

Misc Types
BOOLEAN
BINARY (Note: Only available starting with Hive 0.8.0)

```
<br/>

### 1. Timestamp 데이터형
* 유닉스 표준시(1970년 1월 1일 자정) 이후의 초로 해석되는 정수형
* 유닉스 표준시 이후의 초로 해석되는 소수점 9자리까지를 나노 초로 가질 수 있는 부동소수점형
* JDBC의 날짜 표현 규칙인 YYYY-MM-DD hh:mm:ss.fffffffff를 따라 해석되는 문자열
* to_utc_timestamp, from_utc_timestamp를 내장 함수로 제공함.<br/><br/>

### 2. Binary 데이터형
* 자료를 2진수로 저장하는 데이터형.
* 보통 이미지, 동영상, 레코드 등을 저장할 때 사용함.<br/><br/><br/>


## 컬렉션 데이터형
```
arrays: ARRAY<data_type> (Note: negative values and non-constant expressions are allowed as of Hive 0.14.)

maps: MAP<primitive_type, data_type> (Note: negative values and non-constant expressions are allowed as of Hive 0.14.)

structs: STRUCT<col_name : data_type [COMMENT col_comment], ...>

union: UNIONTYPE<data_type, data_type, ...> (Note: Only available starting with Hive 0.7.0.)
```
<br/>

* 컬렉션 데이터형은 정규화를 깰 수 있기에 대부분의 관계형 데이터베이스에서는 지원하지 않음. 
* 정규화를 깸으로써 발생하는 문제 -> 데이터 중복, 저장 공간 낭비, 잠재적 데이터의 불일치 등
* 빅데이터 시스템은 높은 처리량을 위해 정규화를 희생함으로써 이득을 취함. 컬렉션 데이터를 이용하면 최소한의 디스크 탐색으로 레코드를 빠르게 검색할 수 있음.
