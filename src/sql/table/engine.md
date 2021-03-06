---
layout: page
title: "06.9.엔진 설정"
--- 

# 엔진설정
---
MySQL은 데이터를 처리할 수 있는 다수의 데이터베이스 엔진이 존재합니다. 여러 개의 데이터베이스 엔진은 MySQL을 보다 유연하고 확장된 형태로 시스템을 운영할 수 있도 록 환경을 제공합니다.  

데이터베이스 엔진의 특성별로 장단점이 있습니다. 자신의 데이터의 성격에 맞는 엔진을 설정하여 사용할 수 있습니다. 
MySQL은 다음과 같은 엔진을 지원합니다.  

* MyISAM 
* InnoDB 
* ISAM 

<br>

## 엔진 확인 
---
현재 테이블에 적용되어 있는 엔진을 확인할 수 있습니다. 

| 쿼리 문법 | 
```sql
show create table 테이블명; 
```

| 콘솔 실습 화면 | 
```
mysql> show create table members;
+---------+------------------------------------------------------------------------------------------+
| Table   | Create Table                                                                                                                                                                                                                                                                                               |
+---------+-----------------------------------------------------------------------------------------+
| members | CREATE TABLE `members` (
  `Id` int(11) NOT NULL AUTO_INCREMENT,
  `LastName` varchar(255) DEFAULT NULL,
  `FirstName` varchar(255) DEFAULT NULL,
  `Address` varchar(255) DEFAULT NULL,
  `City` varchar(255) DEFAULT NULL,
  `Country` varchar(255) DEFAULT NULL,
  `manager` varchar(100) DEFAULT NULL,
  `email` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`Id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8 |
+---------+------------------------------------------------------------------------------------------+
1 row in set (0.01 sec)

```

현재 테이블이 InnoDB로 설정되어 있다는 것을 표시합니다.  

<br>

## 엔진 변경 
---
테이블의 엔진 설정은 처음에 테이블을 생성할 때 지정합니다. 하지만 이렇게 설정한 테이블은 나중에 다른 엔진으로 변경할 수 있습니다.  

| 쿼리 문법 | 
```sql
ALTER TABLE 데이블명 ENGINE=엔진명 
```

| 콘솔 실습 화면 | 
```
mysql> alter table members ENGINE=MyISAM;
Query OK, 3 rows affected (0.04 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

기존에 `InnoDB`로 설정되어 있던 엔진을 `MyISAM`으로 변경했습니다.  

<br>

## PHP 코드 
---
PHP를 통하여 엔진 변경 메서드를 생성하도록 하겠습니다.  

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다.  
```php
// 테이블 엔진을 설정합니다.
public function setEngine($tbname,$engine="InnoDB")
{
            if ($tbname) {
                $queryString = "ALTER TABLE $tbname ENGINE=$engine";
                
                // 쿼리를 전송합니다.
                if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
                    $this->msgEcho("쿼리성공] ".$queryString);
                    $this->msgEcho(" 엔진변경($engine)!");

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

예제 파일 | sql-17.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 테이블 엔진을 변경합니다.
	$tbname = "members";
	$db->setEngine($tbname,"MyISAM");

?>

```

화면 출력 
```
mysql connected!
쿼리성공] ALTER TABLE members ENGINE=MyISAM
엔진변경(MyISAM)!
```