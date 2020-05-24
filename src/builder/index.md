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

<br>

## 데이터베이스 접속
---
jinyMysql은 PDO 접속을 쉽게 처리 할 수 있는 Connection 클래스를 제공합니다. [학습하기](connect)

<br>

## 스키마
---
mysql 데이터베이스는 복수의 `schema`를 생성관리 할 수 있습니다. [학습하기](schema)

* [create()](schema) : 스키마를 생성합니다.
* [list()](schema) : 스키마의 목록을 출력합니다.
* [is()](schema) : 스키마의 존재여부를 확인합니다.
* [totalTables()](schema) : 스키마의 테이블 갯수를 반환합니다.

<br>

## 테이블
---
테이블을 생성 합니다.`table()` 메소드는 별도의 테이블 객체와의 관계를 형성합니다. [학습하기](table)

<br>

## 데이터 목록
---
[학습하기](select)
<br>

## 데이터 삽입
---
[학습하기](insert)
<br>

## 테이터 수정
---
[학습하기](update)
<br>

## 데이터 삭제
---
[학습하기](delete)
<br>




