---
layout: page
title: "데이터베이스 목록"
keyword: "jinyphp, mysql"
breadcrumb:
    - "Sql"
    - "Database"
    - "list"
--- 
# 데이터베이스 목록
<hr>

데이터베이스의 이름은 중복하여 사용할 수 없습니다. 또한 MySQL은 데이터베이스명이라는 그룹을 통하여 여러 개의 데이터베이스를 관리할 수 있습니다.  

여러 개의 데이터베이스 명을 포함한 MySQL 시스템은 아주 흔합니다. 1개의 서버에 1개의 DB명만 가지고 있는 경우는 없을 것입니다. 호스팅과 같은 회사는 1개의 MySQL 시스템에 수백 개의 DB명을 가지고 있고, 이를 각각의 사용자에게 할당하여 호스팅을 제 공하고 있습니다.  

<br>
<a name="1"></a>

## 쿼리 실습 
<hr>

MySQL은 자신이 가지고 있는 데이터베이스의 이름 목록을 출력하는 SHOW DATA BASE 명령어를 지원합니다.  

|쿼리 문법| 
```sql
SHOW DATABASE; 
```
`SHOW DATABASE;` 문법은 현재 생성되어 있는 데이터베이스의 이름 목록 전체를 출력합니다.  

|콘솔 실습 화면| 
```sql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| jiny               |
| mysql              |
| performance_schema |
| test               |
+--------------------+
5 rows in set (0.01 sec)
```

위처럼 방금 생성한 `jiny` 데이터베이스명도 함께 포함된 전체 목록을 확인할 수 있습니다.  

<br>
<a name="2"></a>

## PHP 실습 
<hr>

실제적으로 SQL 쿼리와 PHP 연동 소스를 통하여 MySQL에 데이터베이스 목록을 출력해 보도록 하겠습니다.  

|PHP 예제| 
mysql.class.php 파일에 메서드 예제를 추가합니다. 새로 추가한 메서드는 데이터베이스 목록을 출력하는 쿼리를 생성하여 결과를 반환합니다.  

```php
// 데이터베이스 목록을 읽어 옵니다
public function showDatabases()
{
	$queryString = "show databases";
	$this->msgEcho($queryString);

	if ($result = mysqli_query($this->dbcon, $queryString)) {
		$rowss = "";
		$row_cnt = mysqli_num_rows($result);
		for ($i=0;$i<$row_cnt;$i++) {
			$rowss[$i] = mysqli_fetch_object($result);
		}

		$result->free();
		return $rowss;
	} 
}
```

예제 파일 | sql-07.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	if ($rowss = $db->showDatabases()) {
		echo "db Count = ". count($rowss) . "<br>";

		for ($i=0;$i<count($rowss);$i++) {
			echo $i."=";            
			echo $rowss[$i]->Database;
			echo "<br>";

			print_r($rowss[$i]);
			echo "<br>";
		}
	}    

?>
```

화면 출력  
```
mysql connected!
show databases
db Count = 6
0=information_schema
stdClass Object ( [Database] => information_schema ) 
1=jiny
stdClass Object ( [Database] => jiny ) 
2=jiny123
stdClass Object ( [Database] => jiny123 ) 
3=mysql
stdClass Object ( [Database] => mysql ) 
4=performance_schema
stdClass Object ( [Database] => performance_schema ) 
5=test
stdClass Object ( [Database] => test ) 
```

<br>
<a name="3"></a>

## 기본 데이터베이스 
<br>

SHOW DATABASE;를 통하여 목록을 확인해 보면 직접 생성된 것 이외에도 기본적으 로 MySQL에서 미리 가지고 있는 데이터베이스명이 있습니다. MySQL은 자체적으로 권 한 및 모델 구조를 유지 관리하기 위해서 사용하는 데이터베이스 그룹이 있습니다.  

* performance_schema 
* information_schema 
* mysql 
* test 

위의 목록 중에 test 데이터베이스는 삭제해도 됩니다. 기본적으로 MySQL에서 test 목적 을 위해서 생성해 놓은 임시 폴더입니다.  

mysql 데이터베이스명에는 MySQL의 사용자, 접속, DB 정보 등을 가지고 있는 중요 정 보 테이블이 들어 있습니다.  

* user 데이블 
* db 테이블 
* 그 외 여러 파일들. 

<br><br>