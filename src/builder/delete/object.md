---
layout: page
title: "delete object 생성 - SQL빌더"
keyword: "delete, mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "builder"
    - "delete"
    - "object"
---

# 객체생성
---
`delete 클래스`를 통하여 객체를 생성합니다. 
`delete 객체`는 connection의 `delete()` 메소드를 통하여 객체의 생성을 요청할 수 있습니다. 
`delete()` 메소드는 심플팩토리 패턴으로 객체의 생성과 공유를 처리합니다.

<br>

## delete() 메소드
---
delete 메소드는 connection 클래스 안에 선언이 되어 있습니다. 
DB Connection 객체를 생성후에 delete 메소드를 호출해 주기만 하면 됩니다.

```php
$db = new \Jiny\Mysql\Connection($dbinfo);
$delete = $db->delete();
```

`Connection` 객체의 delete 메소드는 delete 클래스의 객체를 생성하기 위한 팩토리 메소드 입니다. 
간단하게 `delete()` 메소드를 호출함으로써 delete 객체를 반환 받을 수 있습니다. 

<br>

### 클래스 확장
---
직접 delete 클래스의 객체를 다음과 같이 생성을 할 수도 있습니다.

```php
$db = new \Jiny\Mysql\Connection($dbinfo);
$delete = new \Jiny\Mysql\Delete($tablename, $db); // 객체를 생성합니다.
```

Delete 객체는 connection 객체와 역의존성을 가지고 있습니다. 관계를 설정하기 위해서 생성자 인자값으로 객체 정보를 전달합니다.

<br>

## 테이블명 설정
---
delete 객체는 테이블의 데이터를 삭제합니다. 그러기 위해서는 객체 내부에 테이블명을 설정해 주어야 합니다. 

메소드의 인자값으로 테이블명을 전달합니다. 입력된 테이블명 객체 생성시에 자동으로 설정합니다.
```php
$delete = $db->delete("members");
```

다음과 같이 테이블 명을 생략한 후에 별도의 setter 메소드를 통하여 테이블을 재설정 할 수 있습니다.
```php
$delete = $db->delete()->setTablename("members");
```

객체 생성후에 setTablename() 메서드를 통하여 설정을 할 수도 있습니다.

<br>
