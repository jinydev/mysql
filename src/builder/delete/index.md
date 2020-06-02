---
layout: page
title: "delete - SQL빌더"
keyword: "delete, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
--- 

# 삭제
---
테이블의 데이터를 삭제합니다. 데이터 삭제는 [delete](/sql/delete) 쿼리문을 기반으로 실행됩니다.

<br>

## Raw SQL을 사용하여 데이터 삭제하기
---
직접 SQL 문장을 작성하여 데이터를 삭제합니다. 또한, 삭제조건을 bind하여 데이터를 삭제할 수 있습니다.  

* [raw 삭제 쿼리](rawsql) 작성
* raw 삭제 쿼리에 데이터 [bind](rawbind)하기

<br>

## delete 빌더 객체
---
직접 raw 쿼리를 사용하여 데이터를 조작하기 위해서는 SQL을 같이 학습해야 합니다. 
또한, SQL을 직접 작성하다 보면 실수로 인하여 문법오류나 오작동을 발생할 수 있습니다.  

Builder는 데이터를 쉽게 삭제할 수 있도록 전용 `delete` 클래스를 제공하며, `Connection` 객체의 `delete()` 메소드를 통하여 확장됩니다.

* [객체생성](object)

* [id삭제](id)
* [전체삭제](all)
<br>



<br>

### 바인드 삭제
---
쿼리에 특정 조건값을 바인드 하여 삭제를 할 수 있습니다.

```php
$stmt = $obj->binds($query, $bind);
$stmt->execute();
```

## where 조건
---

```php
$delete = $db->delete("members4");
$delete->setWhere("id")->build()->run(['id'=>29]);
```

## TRUNCATE
---

```php
$delete = $db->delete("members4")->truncate();
```