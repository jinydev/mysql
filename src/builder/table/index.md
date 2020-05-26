---
layout: page
title: "table - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "Table"
--- 

# 테이블
---
데이터베이스 테이블을 생성합니다.

* raw쿼리
* [테이블 삭제](drop)

## 테이블 객체
---

* [테이블 객체생성](object)
* [컬럼수정](colums)


## 테이블 목록
---
스키마에 존재하는 테이블의 목록을 확인 합니다. [학습하기](list)
* list

<br>

## 테이블생성
---
스키마에 새로운 테이블을 생성합니다. 
테이블은 직접 SQL 쿼리 또는 생성 메소드를 통하여 생성할 수 있습니다. [학습하기](create)

* empty, createEmpty
* create

<br>

## 테이블 확인
---
테이블이 존재하는지 확인을 할 수 있습니다.

```php
public is($name) : bool
```

예제코드: table-is.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 목록출력
$name = "members1";
if ($db->table()->is($name)) {
    echo $name. "테이블이 존재합니다.\n";
} else {
    echo $name. "테이블이 없습니다.\n";
}
```

|실행결과|
```console
$ php table-is.php 
members1테이블이 존재합니다.
```

<br>

## desc() : 테이블 구조
---
테이블의 구조를 확인할 수 있습니다.

|예제코드| table-desc.php
```php
<?php
require "../../loading.php"; // 오토로딩

// 데이터베이스 설정값
$dbinfo = \jiny\dbinfo();

// 설정값, 생성자 인자값으로 전달합니다.
$db = new \Jiny\Mysql\Connection($dbinfo);

// 테이블 구조
$rows = $db->table("members2")->desc();
print_r($rows);
```

|실행결과|
```console
$ php table-desc.php
Array
(
    [0] => Array
        (
            [Field] => id
            [Type] => int(11)
            [Null] => NO
            [Key] => PRI
            [Default] =>
            [Extra] => auto_increment
        )

    [1] => Array
        (
            [Field] => created_at
            [Type] => datetime
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

    [2] => Array
        (
            [Field] => updated_at
            [Type] => datetime
            [Null] => YES
            [Key] =>
            [Default] =>
            [Extra] =>
        )

)
```
실행 결괏값은 2차원 배열로 출력됩니다. 1차 index 배열값은 각 컬럼을 의미합니다.
2차 연상배열은 컬럼의 정보값을 의미합니다.

<br>


## 데이터 갯수 확인
---
확장된 테이블 객체를 활용하여 데이터의 갯수를 확인합니다. 데이터의 갯수는 primary key로 설정된 id 컬럼의 갯수를 체크합니다.

```php
/**
 * 데이터 갯수 확인
 */
$count = $db->table("board")->count();
echo "데이터 갯수=".$count;
```

`count()` 메소드는 테이블의 전체 데이터의 갯수를 반환합니다. 

<br>

## info
---
테이블의 정보를 확인합니다.

```php
info($name)
```

## rename
---
테이블의 이름을 변경합니다.

```php
rename($old, $new);
```

<br>



