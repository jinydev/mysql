---
layout: page
title: "TRUNCATE"
--- 

# TRUNCATE
---
기존 테이블 삭제 명령의 경우 단점은 테이블과 데이터를 모두 삭제한다는 것입니다. 만일 테이블은 남기고 안에 있는 데이터만 모두 삭제하고 싶을 때는 어떻게 해야 할까요 ?  

테이블을 삭제하고 다시 신규 테이블 생성 명령을 실행할 수도 있습니다. 하지만 이것은 DB 시스템에 두 번의 쿼리 명령으로 불필요한 작업을 수행시킬 수 있습니다.  

이런 처리 요청을 위해 새로운 쿼리 명령 TRUNCATE TABLE 을 사용할 수 있습니다.  

| 쿼리 문법 | 
```sql
TRUNCATE TABLE 테이블명; 
```

`TRUNCATE TABLE` 명령은 기존의 테이블의 정보는 유지한 채로 안에 있는 데이터만 초기화합니다.  

<br>

## 콘솔 실습 
---
기존 members 테이블에는 데이터가 존재합니다.  

| 예제 쿼리 | 
```sql
TRUNCATE TABLE members; 
```

| 콘솔 실습 화면 | 
```sql
mysql> select * from members;
+----+----------+-----------+----------+-------+---------+
| Id | LastName | FirstName | Address  | City  | Country |
+----+----------+-----------+----------+-------+---------+
|  1 | hojin    | lee       | shinchon | seoul | Korea   |
+----+----------+-----------+----------+-------+---------+
1 row in set (0.00 sec)

mysql> truncate table members;
Query OK, 0 rows affected (0.02 sec)

mysql> select * from members;
Empty set (0.00 sec)

```

`TRUNCATE TABLE members;`는 `members` 테이블 안에 있는 데이터만 삭제하고 테 이블 자체는 남겨두고 있습니다. 다시 데이터를 조회해 보면 비어 있는 것을 확인할 수 있 
습니다.  

<br>

## PHP 코드 
TRUNCATE TABLE 명령을 PHP 메서드로 추가하여 실습을 해보도록 합시다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다.  
```php
public function clearTable($tbname)
{
            if ($tbname) {
                $queryString = "TRUNCATE TABLE $tbname;";
                $this->msgEcho($queryString);

                // 쿼리를 전송합니다.
                if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
                    $this->msgEcho("쿼리성공] ".$queryString);
                    $this->msgEcho(" 테이블 초기화!");

                    // 객체 반환, 매서드체인
                    return $this; 

                } else {
                    $this->msgEcho("Error] ".$queryString);
                } 

            } else {
                $this->msgEcho("Error] 테이블 이름이 없습니다.");
            }
}
```

예제 파일 | sql-15.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 데이터베이스 삭제합니다.
	$tbname = "members1";
	$db->clearTable($tbname);

?>
```

화면 출력 
```
mysql connected!
TRUNCATE TABLE members1;
쿼리성공] TRUNCATE TABLE members1;
테이블 초기화!
```
