---
layout: page
title: "table - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "Table"
    - "object"
---

# 테이블 객체
---
`jinyMysql`의 table 객체를 통하여 SQL쿼리문을 작성하지 않고도 테이블을 생성할 수 있습니다.

<br>

## 테이블 객체
---
conntection 클래스는 필요한 테이블 데이터 작업을 위해서 클래스를 동적 확장합니다.
table() 메소드는 테이블 객체를 확장하는 플라이웨이트 패턴 입니다. 인자값으로 테이블명을 전달합니다.

```php
$db->table("테이블명");
```

<br>

## 기본 필드
---
빌더를 통하여 테이블을 생성할때에는 몇가지 기본적인 필드가 같이 생성이 됩니다.

### 프라이머리키
모든 테이블은 프라이머리 키를 가지고 있습니다. 프라이머리 키의 이름은 `id`입니다.

```sql
`id` int(11) NOT NULL AUTO_INCREMENT
```

기본값인 `id` 컬럼명은 table class에 상수로 선언이 되어 있습니다. 이를 수정하시면, 다른 프라이머리 키로 테이블을 생성할 수 있습니다.

```php
const PRIMARYKEY = 'id';
```

### created_at, updated_at
---
테이블은 모든 테이블의 자료 삽입일자와 갱신일자를 추적하기 위해서 두개의 특수한 컬럼을 추가합니다.
* created_at : 최초로 삽입된 데이터의 일자를 기록합니다.
* updated_at : 마지막 수정한 데이터의 일자를 기록합니다.

<br>


