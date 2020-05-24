---
layout: page
title: "최신 Id 확인"
--- 

# 최신 Id 확인
---
테이블에는 기본적으로 각각의 열을 구분하는 프라이머리 키 컬럼이 있습니다. 또한 이 키 값은 자동증가 제약사항 속성이 설정되어 있습니다. 자동 증가되는 프라이머리 키는 새로운 데이터를 삽입할 때마다 + 1씩 증가가 됩니다. 또한 새로운 데이터를 저장할 때 프 라이머리 키 값은 자동 증가되기 때문에 생략하고 저장합니다.  

이렇게 생략된 프라이머리 키 값을 새로운 데이터 저장 후에 확인할 수 있습니다. 최신 증 가된 프라이머리 키 값을 확인하는 이유는 데이터 삽입과 동시에 삽입한 데이터를 수정, 다른 테이블에 연결하는 등의 작업이 필요한 경우입니다.  

<br>

## PHP 실습 
---
새롭게 추가된 데이터의 최신 프라이머리 Id는 PHP의 제공된 함수를 통하여 확인할 수 있습니다.  

|PHP 예제| 
mysql.class.php 파일에 메서드 예제를 추가합니다. 
```php
// 마지막 삽입된 Id 값 확인
public function insertId(){
            return mysqli_insert_id($this->dbcon);
}
```

|예제 파일| insert-02.php 
```php
<?php

	include "dbinfo.php";
	include "mysql.class.php";
 
	// ++ Mysqli DB 연결.
	$db = new JinyMysql();

	// 어레이 배열의 키/값을 통하여 데이터를 삽입합니다.
	$tbname = "members";
	$arr = array('FirstName' => "jiny", 'LastName' => "123400");
	$db->arrInsert($tbname,$arr);

	echo "마지막 Id = ".$db->insertID();

?>

```

화면 출력 
```
mysql connected!
FirstName
LastName
쿼리성공] INSERT INTO members (`FirstName`,`LastName`) VALUES ('jiny','123400');
데이터 삽입!
마지막 Id = 7
```
