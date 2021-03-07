---
layout: post
title: "Oracle Parallel"
categories:
- Database
---

## Oracle Hint
---
SQL 튜닝의 핵심 부분임. 일종의 지시 구문.<br/>
힌트를 사용하여 Oracle Optimizer의 쿼리 실행 계획을 바꿀 수 있음.<br/>
주석에 +붙여서 /*+ 힌트 구문 */으로 사용함. <br/>
주석이기에 오타가 있어도 에러가 발생하지는 않지만 대신 힌트가 수행이 안됨.<br/><br/><br/>

## Oracle parallel
---
대용량 테이블에 쿼리를 날릴 때 속도가 매우 느림.<br/> 
한 개의 SQL 쿼리를 한 개의 프로세스로 처리하는데 빨리 실행하기 위해 프로세스 8개, 16개, 32개 등으로 병렬 수행할 수 있음.<br/> 무한정으로 프로세스 개수 늘릴 수 있는 것은 아님.<br/>
우리 팀에 할당된 최대 프로세스 개수 이하로 사용해야 전체 시스템에 이상이 발생하지 않음.<br/><br/><br/>


### 사용 예시
    SELECT /*+ PARALLEL(A 8) */ … FROM 테이블 명 A …
