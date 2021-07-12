---
layout: post
title: "하이브 저장 포맷"
categories:
- Hive
---

## 하이브 저장 포맷
---
* Hive는 두 개의 차원, 즉 **로우 포맷(Row Format)**과 **파일 포맷(File Format)**으로 테이블 저장소를 관리함.<br/> 
* 파일 포맷은 **레코드**가 **파일 안에서 인코딩 되는 방식**이며 레코드 포맷은 **바이트 열**이 **레코드 안에서 인코딩 되는 방식**.<br/><br/><br/>


## Hive DDL 문에서의 저장 포맷 
* DDL문에서 row format고 file format을 설정할 수 있음 (STORED AS DIRECTORIES아래 ROW FORMAT FILE_FORMAT 참고).<br/><br/>
```
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name    -- (Note: TEMPORARY available in Hive 0.14.0 and later)
[(col_name data_type [column_constraint_specification] [COMMENT col_comment], ... [constraint_specification])]
[COMMENT table_comment]
[PARTITIONED BY (col_name data_type [COMMENT col_comment], ...)]
[CLUSTERED BY (col_name, col_name, ...) [SORTED BY (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS]
[SKEWED BY (col_name, col_name, ...)                  -- (Note: Available in Hive 0.10.0 and later)]
ON ((col_value, col_value, ...), (col_value, col_value, ...), ...)
[STORED AS DIRECTORIES]
[
[ROW FORMAT row_format] 
[STORED AS file_format]
| STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]  -- (Note: Available in Hive 0.6.0 and later)
]
[LOCATION hdfs_path]
[TBLPROPERTIES (property_name=property_value, ...)]   -- (Note: Available in Hive 0.6.0 and later)
[AS select_statement];   -- (Note: Available in Hive 0.5.0 and later; not supported for external tables)

```
<br/><br/><br/>


## Hive에서 HDFS 파일 읽고 쓰기
---
다음으로 Hive가 파일 포맷과 로우 포맷을 이용하여 파일을 읽고 쓰는 방법을 설명하겠습니다.<br/>
하이브는 파일 포맷 클래스를 사용하여 HDFS 파일을 읽고 씁니다.<br/>
그리고 Serializer/Deserializer의 약자인 SerDe 클래스를 사용하여 데이터를 직렬화/역직렬화 합니다.<br/><br/>

간단하게 표현 하자면.. 다음과 같습니다.<br/><br/>

* 파일 읽기: HDFS files --> InputFileFormat --> <key, value> --> Deserializer --> Row object 
* 파일 쓰기: Row object --> Serializer --> <key, value> --> OutputFileFormat --> HDFS files <br/><br/>

키 부분은 읽을 때 무시되고 쓸 때는 항상 상수임. 기본적으로 행 객체는 값에 저장됨.<br/>
Hive의 한가지 원칙은 Hive가 HDFS 파일 형식을 소유하지 않음. <br/>
Hive는 현재 FileFormat 클래스를 사용하여 HDFS 파일을 읽고 씀.<br/>
Hive는 SerDe 클래스를 사용하여 데이터를 직렬화 및 역직렬화 함.<br/><br/>

