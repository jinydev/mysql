---
layout: page
title: "잠금"
keyword: "jinyphp, mysql"
breadcrumb:
    - "연동"
    - "Lock"
--- 

# 잠금
---
데이터베이스 시스템이 파일 시스템보다 효율적이고 향상된 점은 다수의 사용자가 동시 에 접속하여 데이터를 처리할 수 있다는 것입니다. 하지만 아무리 좋은 데이터베이스 관 리 시스템 이어도 순간적으로 여러 사람들이 동일한 데이터를 접근할 때는 문제가 발생할 수 있습니다.  

접근의 우선순위에 따라서 데이터가 순간적으로 변경되거나, 데이터의 값에 오류가 발생 할 수 있습니다. 특히 데이터를 변경할 때 동시 접속에 의한 문제가 발생할 수 있습니다.  

<br>

## 잠금 
---
테이블의 데이터를 조작할 때 권한을 통하여 일부 동작들을 제한할 수 있습니다. 테이블 을 잠금을 설정합니다.  

| 쿼리 문법 | 
```sql
LOCK TABLES 테이블명 옵션 
```

옵션 종류 
* READ: SELECT 명령만 가능합니다. 다른 작업들의 명령은 할 수 없습니다. 
* READ_LOCAL: 로컬만 읽기 가능합니다. 
* WRITE: LOCK을 실행한 이외의 사용자는 제한합니다. 

| 콘솔 실습 화면 | 
```sql
mysql> lock tables members read;
Query OK, 0 rows affected (0.00 sec)
```

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 
```php
// 테이블 잠금
// 매개인자: 데이블명, 옵션 = 옵션이 없을 경우 read로 설정합니다.
// 반한값 : 객체 this를 반환 합니다.
public function tableLock($tableName, $option="read")
{
            
            $queryString = "LOCK TABLES ";
            if ($tableName) {
                
                $queryString .= $tableName;
 
                // 옵션이 없는 경우에는 READ로 기본설정 합니다.
                $queryString .= " ".$option;
                
                // 쿼리를 전송합니다.                
                if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
                    $this->msgEcho("쿼리성공] ".$queryString);
                    $this->msgEcho($tableName." LOCK!");
                
                } else {
                    $this->msgEcho("Error] ".$queryString);
                }    
 
                // 객체 반환, 매서드체인
                return $this;
               
            }
            
}

```

<br>

## 해제 
---
향후 정상적인 데이터 처리를 위해서 반드시 잠금된 테이블은 사용 후에 해제해야 합 니다. 잠금 해제 쿼리는 잠금 설정과 달리 별도의 테이블을 선택하지 않습니다. 해제 쿼 리는 잠금 설정된 모든 테이블을 동시에 해제하게 됩니다.  

| 쿼리 문법 | 
```sql
UNLOCK TABLES 
```

| 콘솔 실습 화면 | 
```
mysql> unlock tables;
Query OK, 0 rows affected (0.00 sec)
 
```

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 
```php
// 테이블 잠금해제        
public function tableUnLock()
{
            
            $queryString = "UNLOCK TABLES ";
          
            // 쿼리를 전송합니다.
            if (mysqli_query($this->dbcon, $queryString)=== TRUE) {
                $this->msgEcho("쿼리성공] ".$queryString);
                $this->msgEcho(" TABLE UNLOCK!");
            } else {
                $this->msgEcho("Error] ".$queryString);
            } 
            
            // 객체 반환, 매서드체인
            return $this;            
}

```

테이블 잠금 및 해제 관련 클래스를 추가하고 이를 이용한 예제를 만들어 실험해 보도록 하겠습니다. 

예제 파일 | sql-05.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 테이블을 잠금설정 합니다.
	$db->tableLock("members");

	// 잠금된 테이블을 해제 합니다.
	$db->tableUnLock();

?>

```

화면 출력 
```
mysql connected!
members LOCK!
TABLE UNLOCK!
```

항상 데이터를 삽입하거나 변경할 때 테이블을 잠금 설정하는 것은 안전한 데이터 조작을 위해 유용합니다. 또한 모든 조작 처리 후에는 반드시 테이블을 다시 해제하도록 합니다.  

<br><br>