---
layout: page
title: "테이블 중복"
--- 

# 테이블 중복확인
---
1개의 동일한 데이터베이스 이름 그룹 안에서 테이블명은 고유한 이름을 가지고 있습 니다. 테이블의 이름은 중복하여 사용할 수 없습니다. 중복한다는 것은 중복된 테이블 파 일을 생성을 하는 것과 같습니다. 만일 중복된 이름의 테이블을 생성할 경우에는 오류 메 시지를 출력합니다.  

데이터베이스 이름 그룹이 다르다면 동일한 이름의 테이블명을 가질 수 있습니다. 즉, 테 이블 이름의 중복 허용 원칙은 같은 데이터베이스 이름 안에서만 제한됩니다.  

테이블의 이름은 설치된 운영체제의 환경에 따라 대소문자를 구분하는 경우도 있습니다. 운영체제별로 다른 부분은 테이블명이 데이터베이스 디렉터리에 파일 형태로 매핑되어 저장되기 때문입니다. 대소문자 구별은 시스템 환경 설정을 통하여 제한할 수 있습니다.  

<br>

## 중복 실험 
---
그럼 일부러 기존에 존재하는 동일한 이름의 테이블명을 실행해 보도록 해봅니다.  

| 예제 쿼리 | 
```sql
CREATE TABLE `members` (
	`Id` int(11) NOT NULL AUTO_INCREMENT,
	PRIMARY KEY (`Id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```

| 콘솔 실습 화면 | 
```sql
mysql> CREATE TABLE `members` (
    -> `Id` int(11) NOT NULL AUTO_INCREMENT,
    -> PRIMARY KEY (`Id`)
    -> ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
ERROR 1050 (42S01): Table 'members' already exists
```

테이블의 이름이 같으면 오류를 발생합니다. 테이블의 컬럼 정보가 다르다고 해서 별도의 테이블로 인지하지는 않습니다. 테이블명이 같으면 같은 테이블 중복으로 처리됩니다.  

<br>

## 중복 확인 
테이블을 생성할 때 테이블명의 중복은 오류로 처리됩니다. PHP를 통하여 테이블의 이 름이 중복되어 있는지 확인하는 코드를 생성해 봅니다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 

```php
public function isTables($tbname)
{
    if ($tbname){

        $dbname = $this->dbname;

        $queryString = "show tables from $dbname like '$tbname'";
        $this->msgEcho($queryString);

        // 쿼리를 전송합니다.
        if ($result = mysqli_query($this->dbcon, $queryString)) {
            if (mysqli_num_rows($result)) {                       

                $row = mysqli_fetch_object($result);
                $result->free();

                $this->msgEcho($tbname."은 존재합니다.");
                return true;

            } else {
                $this->msgEcho($tbname."이 없습니다. 생성이 가능합니다.");
                return false;
            }

        } else {
            $this->msgEcho("Error] ".$queryString);
        }

    } else {
        $this->msgEcho("Error] 테이블이 존재합니다.");
    }
}
```

예제 파일 | sql-13.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	$db->dbname = "jiny";
	$tbname = "members123";

	if ($db->isTables($tbname)){
		echo $tbname." 존재하는 테이블 이름입니다.";
	} else {
    	
	}

?>
```

화면 출력 
```
mysql connected!
show tables from jiny like 'members123'
members123은 존재합니다.
members123 존재하는 데이터베이스 이름입니다.
```