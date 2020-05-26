---
layout: page
title: "offset - sql"
---

# offset
---
데이터의 출력 개수를 제어하는 OFFSET 키워드가 있습니다. OFFSET은 LIMIT를 이용 하여 부분 출력하는 동작은 비슷합니다.  

| 쿼리 문법 | 
```sql
SELECT 컬럼명, 컬럼명, … FROM 테이블명 LIMIT 레코드 수 OFFSET 이동 레코드 수; 
```

데이터를 출력할 때 OFFSET 수만큼 이동한 다음에 지정한 레코드 수만큼을 출력합니다.  

<br>

## 콘솔 실습 
---
LIMIT 에서 처음에 이동하는 시작점을 OFFSET 부분의 위치로 이동한 것과 비슷합니다.  

| 예제 쿼리 | 
```sql
select code from orders limit 3 offset 3; 
```

주문 목록에서 오프셋 위치를 3으로 이동합니다. 이동 시점에서 연속된 데이터 3개를 읽 어서 출력합니다.  

| 콘솔 실습 화면 | 
```sql
mysql> select code from orders limit 3 offset 3; +-------+ | code | +-------+ | O_004 | | O_005 | | O_006 | +-------+ 3 rows in set (0.00 sec) 
```

데이터를 3만큼 시작 위치를 이동한 상태에서 3개의 데이터만 출력합니다. 즉 LIMIT 3, 3과 비슷합니다.  

<br>

## PHP 실습 
---
PHP 코드를 통하여 OFFSET 처리에 대한 실습을 합니다. 

| PHP 예제 | 
mysql.class.php 파일에 메서드 예제를 추가합니다. 
```php
// 지정한 위치많큼 이동후, 갯수를 출력합니다.
public function offset($query, $a, $b){
            $queryString = $query . " limit $b offset $a";
            return $queryString; 
}
 
```

예제 파일 | offset-01.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 기본 select 쿼리
	$query = "SELECT Id, FirstName, LastName FROM members";
	// 기본쿼리에 2만큼 이동후 3개를 출력함.
	$queryString = $db->offset($query,2,3);
    
	if($rowss = $db->selectRowss($queryString)){
		echo "tables fields = ". count($rowss) . "<br>";
 
		for($i=0;$i<count($rowss);$i++){
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
쿼리성공] SELECT Id, FirstName, LastName FROM members limit 3 offset 2
tables fields = 3
0=stdClass Object ( [Id] => 3 [FirstName] => kim [LastName] => james )
1=stdClass Object ( [Id] => 5 [FirstName] => jiny [LastName] => 1234 )
2=stdClass Object ( [Id] => 6 [FirstName] => jiny [LastName] => 1234 ) 
```
