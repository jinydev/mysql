---
layout: page
title: "REPLACE"
--- 

# REPLACE
---
INSERT 쿼리를 생성할 때 중복을 허용하지 않는 프라이머리 키나 인덱스는 실행되지 않 습니다. 하지만 REPLACE 명령문은 중복된 인덱스 컬럼이 있을 경우 기존 데이터를 삭제 하고 새로운 데이터로 교체하게 됩니다.  

먼저 테이블의 데이터 내용을 확인해 봅니다.  

| 콘솔 실습 화면 | 
```sql
mysql> select * from board;
+----+---------+-------+-------+------+
| Id | regdate | title | level | pos  |
+----+---------+-------+-------+------+
|  2 | NULL    | NULL  |     2 |    5 |
|  3 | NULL    | NULL  |     1 |    2 |
+----+---------+-------+-------+------+
2 rows in set (0.00 sec)
```

Id가 2로 중복된 데이터를 REPLACE로 삽입해 봅니다.  

| 콘솔 실습 화면 | 
```sql
mysql> REPLACE INTO board (Id, level,pos) values (2,21,53);
Query OK, 2 rows affected (0.01 sec)

```
오류가 나지 않고 정상적으로 수행되었습니다. Selelct 명령을 통하여 다시 한번 내용을 확인해 봅니다. 

| 콘솔 실습 화면 | 
```sql
mysql> select * from board;
+----+---------+-------+-------+------+
| Id | regdate | title | level | pos  |
+----+---------+-------+-------+------+
|  2 | NULL    | NULL  |    21 |   53 |
|  3 | NULL    | NULL  |     1 |    2 |
+----+---------+-------+-------+------+
2 rows in set (0.00 sec)

```
위의 실습에서는 인덱스가 2인 동일한 컬럼을 REPLACE를 통하여 기존에 데이터가 삭제 되고 새로운 데이터로 변경되는 것을 확인할 수 있습니다.  
