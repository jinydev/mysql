---
layout: page
title: "update - SQL빌더"
keyword: "update, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "update"
    - "object"
---

# Object 객체를 통한 쿼리빌드
`jinyMysql`은 손쉬운 데이터 갱신 작업을 위해서 Update 클래스를 제공합니다.

<br>

## 객체생성
---
update 객체는 Connection 클래스의 `update` 팩토리 메소드를 호출함으로서 객체를 반환 받을 수 있습니다. 

* 기본호출 :

```php
$db->update();
```
`update()` 메소드는 update 클래스의 객체를 생성하여 반환합니다.

* 첫번째 인수값 : 첫번째 인수로 테이블명을 지정하는 경우, 객체를 생성시 자동으로 테이블명을 설정합니다.

```php
uptate("members");
```

* 두번재 인자 : 
갱신할 데이터를 전송합니다.

```php
uptate("members", ['firstname'=>"1234"]);
```
갱신데이터는 객체 생성후에 `setFields()`메소드를 사용하여 추가 설정이 가능합니다.

<br>


