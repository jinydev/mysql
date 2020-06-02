---
layout: page
title: "SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
--- 

# SQL Builder
---
`jinyMysql`은 쿼리를 쉽게 생성 처리할 수 있는 SQL Builder 입니다.

패키지 설치 
```console
composer require jiny/mysql
```

<br>

## 데이터베이스 접속
---
jinyMysql은 PDO 접속을 쉽게 처리 할 수 있는 Connection 클래스를 제공합니다. [학습하기](connect)

<br>


## Raw SQL
---
빌더를 동하여 보다 간편하게 raw SQL 쿼리를 실행할 수 있습니다. [>>학습하기](raw)

* 쿼리설정
* bind 값 결합
* 실행

<br>

## 스키마
---
mysql 데이터베이스는 복수의 `schema`를 생성관리 할 수 있습니다. [학습하기](schema)

`schema()`메소드를 통하여 빌더 객체를 생성할 수 있습니다. 
```php
$db->schema();
```

* [create()](schema) : 스키마를 생성합니다.
* [list()](schema) : 스키마의 목록을 출력합니다.
* [is()](schema/is) : 스키마의 존재여부를 확인합니다.
* [totalTables()](schema/totaltables) : 스키마의 테이블 갯수를 반환합니다.

<br>

## 테이블
---
테이블을 생성 합니다.
`table()` 메소드는 별도의 테이블 객체와의 관계를 형성합니다. [>>학습하기](table)

`table()`메소드를 통하여 빌더 객체를 생성할 수 있습니다. 
```php
$db->table();
```

* 테이블 [목록](table/list)
* 테이블 [생성](table/create)
* 테이블 [삭제](table/drop)
* [코멘트](table/comment)

* [컬럼변경](table/colums)
* 컬럼 코멘트

<br>

## 데이터 목록
---
테이블의 데이터를 조회합니다. rawSQL 또는 select 클래스를 통하여 데이터를 조회할 수 있습니다. [>>학습하기](select)

`select()`메소드를 통하여 빌더 객체를 생성할 수 있습니다. 
```php
$db->select();
```

* rawSQL 작성하기
* select 클래스 사용하기

* [값 읽어오기](select/fetch)

<br>

## 데이터 삽입
---
테이블에 새로운 데이터를 삽입합니다. rawSQL 또는 insert 클래스를 통하여 데이터를 삽입할 수 있습니다. [학습하기](insert)

`insert()`메소드를 통하여 빌더 객체를 생성할 수 있습니다. 
```php
$db->insert();
```

* rawSQL 작성하기
* insert 클래스 사용하기

> [삽입 SQL 학습하기](/sql/insert)

<br>

## 테이터 수정
---
등록된 데이터를 수정합니다. rawSQL 또는 update 클래스를 통하여 데이터를 수정할 수 있습니다.
[학습하기](update)

`update()`메소드를 통하여 빌더 객체를 생성할 수 있습니다. 
```php
$db->update();
```

* rawSQL 작성하기
* update 클래스 사용하기

<br>

## 데이터 삭제
---
테이블에 있는 데이터를 삭제합니다. rawSQL 또는 delete 클래스를 통하여 쿼리를 실행할 수 있습니다.
[학습하기](delete)

`delete()`메소드를 통하여 빌더 객체를 생성할 수 있습니다. 
```php
$db->delete();
```

* rawSQL 작성하기
* delete 클래스 사용하기

<br>


