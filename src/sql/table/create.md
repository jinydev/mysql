---
layout: page
title: "Table Create - learn Mysql | JinyDev"
keyword: "coulumes, table, sql"
description: "테이블을 생성하는 방법에 대해서 알아 봅니다."
breadcrumb:
    - "sql"
    - "table"
    - "create"
--- 

# 테이블 생성(Create)
---
SQL 명령문을 통하여 실제적인 테이블을 생성해 봅니다. 테이블 생성은 테이블명과 소괄 호( ) 안에 컬럼 정보를 같이 선언하면 됩니다.  

```sql
CREATE TABLE 테이블명 (   
    컬럼정보…
)
```

테이블 생성 시 들어가는 컬럼은 컬럼명, 데이터타입, 컬럼속성 세 가지의 값을 한 줄로 선 언하면 됩니다. 또한 여러 개의 컬럼 설정은 콤마(,)로 구분합니다.  

```
컬럼명 데이터 타입 컬럼 속성, 
```

컬럼 속성은 생략 가능합니다. 하지만 하나의 테이블에는 반드시 프라이머리 (Primary)키 속성을 가지고 있는 컬럼을 포함하고 있어야 합니다. 주로 프라이머리 키로 컬럼명을 ‘id’ 로 사용하는 경우가 많습니다. 프라이머리 키는 각 레코드 데이터는 중복되지 않는 유일 한 키 값을 가지고 있습니다.  

<br>

## 콘솔 실습
--- 
다음 예제 쿼리는 회원 목록을 담고 있는 테이블입니다. SQL 쿼리를 통하여 테이블을 생 성해 봅니다.  

| 예제 쿼리 | 
```sql
CREATE TABLE `members` ( 
`Id` int(11) NOT NULL AUTO_INCREMENT, 
LastName varchar(255), 
FirstName varchar(255), 
Address varchar(255), 
City varchar(255), 
Country varchar(255), 
PRIMARY KEY (`Id`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8; 
```

예제 쿼리를 콘솔에 입력하여 테이블을 생성하도록 실습하겠습니다.  

| 콘솔 실습 화면 | 
```sql
mysql> CREATE TABLE `members` (
    -> `Id` int(11) NOT NULL AUTO_INCREMENT,
    -> LastName varchar(255),
    -> FirstName varchar(255),
    -> Address varchar(255),
    -> City varchar(255),
    -> Country varchar(255),
    -> PRIMARY KEY (`Id`)
    -> ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.04 sec)
```

테이블 생성 시 추가로 DB 엔진과 언어 세트를 함께 설정하여 생성할 수도 있습니다. 이 에 대해서는 다음에 다시 설명 하겠습니다. 

<br>

## PHP 실습 
---
PHP를 통하여 소스상에서 쿼리 전송을 통한 테이블을 생성하도록 하겠습니다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 테이블을 생성하는 메서드를 추가 
합니다.
```php
// 테이블 생성
public function createTable($queryString){
            $this->msgEcho($queryString);

            // 쿼리를 전송합니다.
            if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
                $this->msgEcho("쿼리성공] ".$queryString);
                $this->msgEcho(" 테이블 생성!");

                // 객체 반환, 매서드체인
                return $this; 

            } else {
                $this->msgEcho("Error] ".$queryString);
            }
}

```

예제 파일 | sql-11.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	$queryString = "
    	CREATE TABLE `members123` (
			`Id` int(11) NOT NULL AUTO_INCREMENT,
			LastName varchar(255),
    			FirstName varchar(255),
    			Address varchar(255),
    			City varchar(255),
			Country varchar(255),
			PRIMARY KEY (`Id`)
		) ENGINE=InnoDB DEFAULT CHARSET=utf8;";

	// 테이블을 생성합니다.
	$db->createTable($queryString);

?>
```

화면 출력 
```
mysql connected!
CREATE TABLE `members123` ( `Id` int(11) NOT NULL AUTO_INCREMENT, LastName varchar(255), FirstName varchar(255), Address varchar(255), City varchar(255), Country varchar(255), PRIMARY KEY (`Id`) ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
쿼리성공] CREATE TABLE `members123` ( `Id` int(11) NOT NULL AUTO_INCREMENT, LastName varchar(255), FirstName varchar(255), Address varchar(255), City varchar(255), Country varchar(255), PRIMARY KEY (`Id`) ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
데이터베이스 삭제!

```

PHP를 통해서 테이블 생성 쿼리를 전송합니다. 실제로 데이터베이스에 테이블이 생성되 었습니다.  

