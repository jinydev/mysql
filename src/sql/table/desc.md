---
layout: page
title: "06.7.테이블 구조 확인"
---

# 테이블 구조
---
우리는 앞에서 테이블의 목록과 테이블의 상세 목록을 출력하는 학습과 실험을 했습니다. 
하지만 테이블의 각각의 컬럼 정보와 속성까지 알기에는 부족합니다.  

새로운 쿼리 명령어 DESC는 테이블의 상세 컬럼 정보까지 확인할 수 있습니다.  

| 쿼리 문법 | 
```sql
DESC 테이블명; 
```

<br>

## 콘솔 실습 
---
DESC 쿼리 명령은 지정한 테이블의 상세한 구조를 확인할 수 있습니다.  

| 예제 쿼리 | 
```sql
DESC members; 
```

| 콘솔 실습 화면 | 
```
mysql> desc members;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Id        | int(11)      | NO   | PRI | NULL    | auto_increment |
| LastName  | varchar(255) | YES  |     | NULL    |                |
| FirstName | varchar(255) | YES  |     | NULL    |                |
| Address   | varchar(255) | YES  |     | NULL    |                |
| City      | varchar(255) | YES  |     | NULL    |                |
| Country   | varchar(255) | YES  |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
6 rows in set (0.02 sec)

```

`DESC` 쿼리 명령은 테이블의 컬럼명, 데이터 타입 및 속성까지 목록으로 출력합니다.  

<br>

## PHP 코드 
---
DESC 쿼리를 통하여 테이블의 컬럼 목록을 출력하는 PHP 코드를 생성해 보도록 하겠습니다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 

```php
// 테이블 정보를 읽어 옵니다
public function descTable($tbname)
{
	$queryString = "desc $tbname";
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

예제파일) sql-16.php
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 테이블 구조를 확인합니다.
	$tbname = "members";
	if ($rowss = $db->descTable($tbname)) {
		echo "tables fields = ". count($rowss) . "<br>";

		for ($i=0;$i<count($rowss);$i++) {
			echo $i."=";            
 			print_r($rowss[$i]);
			echo "<br>";
		}
	}    

?>

```

화면 출력
``` 
mysql connected!
desc members
tables fields = 8
0= stdClass Object ( [Field] => Id [Type] => int(11) [Null] => NO [Key] => PRI [Default] => [Extra] => auto_increment )
1= stdClass Object ( [Field] => LastName [Type] => varchar(255) [Null] => YES [Key] => [Default] => [Extra] => )
2= stdClass Object ( [Field] => FirstName [Type] => varchar(255) [Null] => YES [Key] => [Default] => [Extra] => )
3= stdClass Object ( [Field] => Address [Type] => varchar(255) [Null] => YES [Key] => [Default] => [Extra] => )
4= stdClass Object ( [Field] => City [Type] => varchar(255) [Null] => YES [Key] => [Default] => [Extra] => )
5= stdClass Object ( [Field] => Country [Type] => varchar(255) [Null] => YES [Key] => [Default] => [Extra] => )
6= stdClass Object ( [Field] => manager [Type] => varchar(100) [Null] => YES [Key] => [Default] => [Extra] => )
7= stdClass Object ( [Field] => email [Type] => varchar(255) [Null] => YES [Key] => [Default] => [Extra] => ) 

```

<br>

## SHOW COLUMNS 
---
DESC 명령어 이외에 SHOW COLUMNS 명령을 통하여 테이블의 구조를 확인할 수도 있습니다.  

| 쿼리 문법 | 
```sql
SHOW COLUMNS FROM 테이블명; 
```

| 콘솔 실습 화면 | 
```
mysql> show columns from members;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Id        | int(11)      | NO   | PRI | NULL    | auto_increment |
| LastName  | varchar(255) | YES  |     |         |                |
| FirstName | varchar(20)  | YES  |     | NULL    |                |
| Address   | varchar(255) | YES  |     | NULL    |                |
| address2  | varchar(255) | YES  |     | NULL    |                |
| City      | varchar(30)  | NO   |     | NULL    |                |
| Country   | varchar(255) | YES  |     | NULL    |                |
| manager   | varchar(100) | YES  |     | NULL    |                |
| email     | varchar(255) | YES  |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
9 rows in set (0.09 sec)
```


