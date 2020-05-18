---
layout: page
title: "테이블 삭제"
--- 

# 테이블 삭제
---
생성한 테이블을 삭제할 수 있습니다. DROP TABLE 쿼리 명령을 통하여 기존에 존재하 는 테이블을 삭제합니다.  

| 쿼리 문법 | 
```sql
DROP TABLES 테이블명; 
```

여러 개의 테이블을 삭제할 수도 있습니다. 

| 쿼리 문법 | 
```sql
DROP TABLE 테이블1, 테이블2; 
```

테이블을 삭제할 때는 주의해야 합니다. 테이블을 삭제하게 되면 테이블 안에 있는 모든 데이터가 삭제됩니다. 또한 삭제된 데이터는 복구가 불가능하기 때문에 매우 신중해야 합 니다.  

테이블 삭제 또한 데이터베이스 삭제에서 사용했던 IF EXISTS를 같이 사용할 수 있습 니다. 테이블이 존재하는 경우에만 삭제가 됩니다.  

| 쿼리 문법 |
```sql 
DROP TABLE IF EXISTS 테이블명; 
```

또는 여러 개의 테이블을 한 번에 삭제할 수도 있습니다. 테이블명을 콤마 (,)로 구분하여 입력하면 됩니다.  

| 쿼리 문법 | 
```sql
DROP TABLE IF EXISTS 테이블1, 테이블2; 
```

<br>

## 삭제 실습 
---
쿼리 명령을 전송하여 테이블을 삭제해 봅니다. 

| 예제 쿼리 | 
```sql
DROP TABLES members; 
```

| 콘솔 실습 화면 | 
```sql
mysql> DROP TABLES members; Query OK, 0 rows affected (0.01 sec) 
mysql> show tables; Empty set (0.00 sec) 
```

기존에 생성되어 있는 `members` 테이블을 `drop` 명령어를 통하여 삭제가 성공되었다는 메시지를 확인할 수 있습니다.  

<br>

## PHP 코드 
---
PHP를 통하여 테이블을 삭제하는 메서드를 만들어 봅니다. 테이블을 삭제할 경우 데이 터도 함께 삭제되는 위험이 있습니다. 만일, 안전한 삭제 코드를 만든다고 한다면 삭제하 
기 전에 데이터가 있지는 확인하는 루틴을 하나 더 삽입해도 좋을 것입니다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다.  
```php
public function dropTable($tbname)
{
            if ($tbname) {
                $queryString = "DROP TABLES $tbname;";
                $this->msgEcho($queryString);

                // 쿼리를 전송합니다.
                if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
                    $this->msgEcho("쿼리성공] ".$queryString);
                    $this->msgEcho(" 테이블 삭제!");

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

예제 파일 | sql-14.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 데이터베이스 삭제합니다.
	$tbname = "members123";
	$db->dropTable($tbname);

?>
```

화면 출력
```
mysql connected!
DROP TABLES members123;
쿼리성공] DROP TABLES members123;
테이블 삭제!
```