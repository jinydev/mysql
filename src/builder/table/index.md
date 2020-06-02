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

## 테이블 객체
---

* [테이블 객체생성](object)
* [컬럼수정](colums)


## 테이블 목록
---
스키마에 존재하는 테이블의 목록을 확인 합니다. [학습하기](list)

* list
* is
* desc
* count

<br>

## 테이블생성
---
스키마에 새로운 테이블을 생성합니다. 
테이블은 직접 SQL 쿼리 또는 생성 메소드를 통하여 생성할 수 있습니다. [학습하기](create)

* empty, createEmpty
* create
* rename

<br>

## 테이블 삭제
---
* [테이블 삭제](drop)


## 초기화
---
추가 설정된 모든 값을 초기화 합니다.

```php
clear();
```

