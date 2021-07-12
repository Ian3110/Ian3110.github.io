---
layout: post
title: "하이브(Hive) 구성요소 및 동작원리"
categories:
- Hive
---


<img src="/assets/img/system_architecture.png" width="90%" height="90%" title="HiveArchitecture" alt="HiveArchitecture"/>
<br/>

*위 그림의 하둡 구성요소는 하둡 버전1입니다.* <br/><br/>

## Hive 구성요소
---
**UI**: CLI나 HWI 등 사용자의 입력을 받는 요소<br/>
**Driver**: 쿼리 입력을 받음. 세션을 관리하고 JDBC/ODBC 인터페이스를 제공함.<br/>
**Complier**: 쿼리를 분석하고 실행 계획을 생성함. 쿼리 블록 및 쿼리 식에 대한 의미 분석을 수행하고 메타스토어에서 조회한 테이블 및 파티션 메타 데이터를 사용하여 실행계획을 생성함.<br/>
**Meta Store**: 컬럼, 컬럼 type 정보, 데이터를 읽고 쓰는 데 필요한 serializers/deserializers 정보, 데이터가 저장되는 HDFS 파일 정보 등을 저장함.<br/>
**Execution Engine**: 컴파일러가 만든 실행 계획을 수행함. Execution Engine은 계획의 종속성을 관리하고 각 단계를 적절한 시스템 구성 요소에 할당하여 작업을 수행시킴.<br/><br/><br/>

## Hive 동작원리
---
UI는 Driver에게 실행 인터페이스를 호출함 (1단계:executeQuery). Driver는 쿼리에 대한 세션을 만들고 쿼리를 Compiler로 보내 실행 계획을 세우게 함 (2단계:getPlan). Compiler는 메타 스토어에서 메타 데이터를 가져오고 쿼리를 분석하여 실행 계획을 세움 (3단계:getMetaData, 4단계:sendMetaData). 세운 계획은 Driver에 전달하고 이는 또 다시 Execution Engine에 전달 됨 (5단계: sendPlan, 6단계:executePlan). Execution Engine은 작업에 맞게 하둡의 적절한 구성 요소로 일 전달함.<br/><br/>
이제부터는 하둡의 맵리듀스 작업이 됨. 각 작업은 임시 HDFS 파일에 저장됨. DML 작업의 경우, 최종 임시 파일이 테이블 위치로 이동함.<br/><br/>
