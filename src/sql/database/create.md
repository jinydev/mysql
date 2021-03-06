---
layout: page
title: "데이터베이스"
keyword: "jinyphp, mysql"
breadcrumb:
    - "Sql"
    - "Database"
    - "create"
--- 

# 데이터베이스 생성
<hr>
데이터베이스 이름은 다수의 테이블을 담고 있는 폴더와 같습니다. 실제적으로 데이터베이스명을 생성하면 MySQL은 해당 데이터 베이스명과 동일한 폴더를 내부적으로 하나 생성하게 됩니다.  

<br>
<a name="1"></a>

## 쿼리 실습 
<hr>

데이터베이스 명의 생성은 CREATE DATABASE 명령을 실행할 수 있습니다. SQL 쿼리 구분을 만들어 MySQL 서버에 전송하면 됩니다.  

|쿼리 문법| 
```sql
CREATE DATABASE 데이터베이스명; 
```

데이터베이스 생성 문법은 2개의 키워드를 같이 사용하여 작성합니다. CREATE + DATABASE로 지정한 이름으로 데이터 베이스를 생성한다는 의미입니다.  

`jiny` 이름이 새로운 데이터베이스를 만들어 봅니다. 

|예제 쿼리| 
```sql
CREATE DATABASE jiny; 
```

|콘솔 실습 화면| 
```
mysql> create database jiny;
Query OK, 1 row affected (0.01 sec)
```

콘솔창을 확인해 보면 Query OK라고 정상적으로 처리가 되었다는 메세지가 출력됩 니다. 또한 처리 쿼리의 개수와 실행 시간을 함께 표시합니다.  

<br>
<a name="2"></a>

## PHP 실습 
<hr>
실제적으로 SQL 쿼리와 PHP 연동 소스를 통하여 MySQL에 새로운 데이터베이스명을 하나 추가하도록 하겠습니다.  

|PHP 예제| 
mysql.class.php 파일에 메서드 예제를 추가합니다. 데이터베이스 생성 쿼리를 만드는 메서드입니다. 

```php
// 데이터베이스 생성
public function createDatabase($dbname)
{
    if ($dbname) {
        $queryString = "CREATE DATABASE $dbname;";
        $this->msgEcho($queryString);

        // 쿼리를 전송합니다.
        if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
            $this->msgEcho("쿼리성공] ".$queryString);
            $this->msgEcho(" 데이터베이스 생성!");

            // 객체 반환, 매서드체인
            return $this; 

        } else {
            $this->msgEcho("Error] ".$queryString);
        } 

    } else {
        $this->msgEcho("Error] 데이터베이스 이름이 없습니다.");
    }
            
}
```

데이터베이스명이 있는지 확인하는 추가 메서드도 하나 더 만들어 봅니다.  

```php
// 데이터베이스명 존재여부 확인
public function isDatabases($dbname)
{
    if ($dbname) {
        $queryString = "show databases like '".$dbname."'";
        $this->msgEcho($queryString);

        // 쿼리를 전송합니다.
        if ($result = mysqli_query($this->dbcon, $queryString)) {
            if(mysqli_num_rows($result)) {                       

                $row = mysqli_fetch_object($result);
                $result->free();

                $this->msgEcho($dbname."은 존재합니다.");
                return true;

            } else {
                $this->msgEcho($dbname."이 없습니다. 생성이 가능합니다.");
                return false;
            }

        } else {
            $this->msgEcho("Error] ".$queryString);
        }

    } else {
        $this->msgEcho("Error] 데이터베이스 이름이 없습니다.");
    }
} 
```

추가한 클래스 메서드를 통하여 실제적인 데이터베이스 생성 코드를 실험해 보도록 합니다.  

예제 파일) sql-06.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	$dbname = "jiny123";
	if ($db->isDatabases($dbname)){
    		echo $dbname." 존재하는 데이터베이스 이름입니다.";
	} else {
    		$db->createDatabase($dbname);
	}
?> 
```

화면 출력 
```
mysql connected!
show databases like 'jiny123'
jiny123이 없습니다. 생성이 가능합니다.
CREATE DATABASE jiny123;
쿼리성공] CREATE DATABASE jiny123;
데이터베이스 생성!
```

<br>
<a name="3"></a>

## 데이터베이스 이름 중복 
<hr>
MySQL에서 데이터베이스 이름은 중복으로 사용할 수 없습니다. 데이터베이스명은 1개 로 유일한 이름을 가지고 있어야 합니다. 따라서 중복된 이름의 데이터베이스 생성을 지 정하면 DB 시스템은 오류를 발생합니다.  

한 번 실수로 기존에 존재하는 동일한 데이터베이스 이름으로 데이터베이스를 생성하는 SQL 명령을 입력해 봅니다.  

|콘솔 실습 화면| 
```sql
mysql> create database jiny;
ERROR 1007 (HY000): Can't create database 'jiny'; database exists
```

위처럼 데이터베이스 이름이 중복되어 생성할 수 없다는 에러 메시지를 출력합니다.  

<br>
<a name="4"></a>

## 대소문자 구별 
<hr>
SQL 키워드는 대소문자를 구별하지 않지만 데이터베이스 이름은 운영체제별로 차이가 있습니다.  
윈도우 운영체제는 데이터베이스 이름에 대해서 대소문자를 구분하지 않습 니다. 하지만 리눅스 계열의 운영체제는 데이터베이스 이름을 대소문자로 구분을 합니다. 이는 리눅스 환경의 특성이라고도 할 수 있습니다.  

<br><br>