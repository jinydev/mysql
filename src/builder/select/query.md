---
layout: page
title: "select - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "select"
    - "query"
---

# 쿼리 생성하기
---
빌더를 통하여 보다 손쉽게 쿼리를 생성할 수 있습니다.

<br>

## 설정하기
---
* setQuery() : 직접 쿼리를 설정합니다.
* getQuery() : 설정된 쿼리 문자열을 읽어 옵니다.
* clearQuery() : 설정된 쿼리를 초기화 합니다.

<br>

## 빌드하기
---
연상배열의 키를 이용하여 select 쿼리를 생성할 수 있습니다.

build 메소드는 입력된 배열정보를 통하여 select 쿼리를 생성하여 객체에 저장에 설정합니다.

```php
$fields = ["id","firstname"];
$query = $db->select("members4")->build($fields)->getQuery();
echo $query;
```

설정된 쿼리는 getQuery()를 통하여 읽어 올 수 있습니다.


```php
$fields = ["id","firstname"];
$select = $db->select("members4")->setField("lastname");
$query = $select->build($fields)->getQuery();
echo $query;
```
기존에 미리 설정된 필드가 있는 경우 합산되어 처리 됩니다.

```console
$ php select-query02.php 
SELECT lastname,id,firstname FROM `db2020`.`members4`;
```

## 조건 추가하기
---
쿼리에 where 조건을 추가합니다.

```php
$select = $db->select("members4")->setField("lastname");
$select->setWhere("id");
$select->setWhere("firstname");
```

복수 조건 설정
```php
$fields = ["id","firstname"];
$select = $db->select("members4")->setField("lastname");
$select->setWheres(["id","firstname"]);
```

조건값 실행하기
run()을 통하여 쿼리를 실행합니다.
```php
$query = $select->build($fields)->getQuery();
$rows = $select->run(['id'=>"1"])->fetchObjAll();
print_r($rows);
```
