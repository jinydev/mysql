---
layout: page
title: "update - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
--- 

# 삭제
---
테이블의 데이터를 삭제합니다. 데이터 삭제는 [delete](/sql/delete) 쿼리문을 기반으로 합니다.

<br>

## Raw SQL을 사용하여 데이터 삭제하기
---
직접 rawSQL을 작성하여 데이터를 삭제합니다. 또한, 삭제조건을 지정할때 데이터를 bind하여 실행을 할 수 있습니다.

* [raw 삭제 쿼리](rawsql) 작성
* raw 삭제 쿼리에 데이터 [bind](rawbind)하기

<br>

## delete 객체
---
직접 raw 쿼리를 사용하여 데이터를 조작하기 위해서는 SQL을 같이 학습해야 합니다. 
또한, SQL을 직접 작성하다 보면 실수로 인하여 문법오류나 오작동을 발생할 수 있습니다.  

Builder는 데이터를 쉽게 삭제할 수 있도록 전용 `delete` 클래스를 제공하며, `Connection` 객체의 `delete()` 메소드를 통하여 확장됩니다.

<br>

### 클래스 확장
---
`Connection` 객체의 delete 메소드는 delete 클래스의 객체를 생성하기 위한 팩토리 메소드 입니다. 
간단하게 `delete()` 메소드를 호출함으로써 delete 객체를 반환 받을 수 있습니다.

<br>

### 객체얻기
---
다음과 같이 delete 메소드를 호출합니다. 메소드의 인자값으로 테이블명을 전달합니다.

```php
$obj = $db->delete("members4");
```

다음과 같이 테이블 명을 생략한 후에 별도의 setter 메소드를 통하여 테이블을 재설정 할 수 있습니다.

```php
$obj = $db->delete();
$obj->setTablename("members4");
```

`setTable()` 메소드는 삭제를 위한 테이블명을 설정합니다.

<br>

### 특정 id 삭제
---
delete 객체를 이용하면 보다 쉽게 데이터를 삭제할 수 있습니다. 
특정 id값을 가지는 테이블을 삭제할 경우 다음과 같이 `id()` 메소드를 호출합니다.

```php
$obj->id(3);
```

<br>

### 예제코드
---

|예제코드| delete-id.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();
$db = new \Jiny\Mysql\Connection($dbinfo);

$dataObj = $db->delete("members4");
$dataObj->id(3);

if ($rows = $db->select("members4")->fetchObjAll()) {
    foreach($rows as $row) {
        foreach($row as $key => $value) {
            echo $key. "=". $value. "\t";
        }
        echo "\n";
    }
} else {
    echo "데이터목록이 없습니다.";
}
```

<br>

### 전체삭제
---
테이블의 전체 데이터를 삭제할 수 있습니다.

```php
$obj->all();
```

<br>

### 바인드 삭제
---
쿼리에 특정 조건값을 바인드 하여 삭제를 할 수 있습니다.

```php
$stmt = $obj->binds($query, $bind);
$stmt->execute();
```
