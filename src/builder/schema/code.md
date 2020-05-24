---
layout: page
title: "schema - SQL빌더"
keyword: "mysql, sql, builder, jinyMysql, jinyPHP"
breadcrumb:
    - "Builder"
    - "schema"
    - "code"
--- 

# 스키마 메소드
---
소스코드를 통하여 어떻게 Connection 겍체가 Schema 객체와의 복합구조를 결합하는지에 대해서 알아 봅니다.

```php
/**
 * 스키마 확장
 */
private $_schema;
public function schema()
{
    // 플라이웨이트 공유객체 관리
    if (!isset($this->_schema)) {
        $this->_schema = new \Jiny\Mysql\Schema($this); // 객체를 생성합니다.
    } else {
        
    }

    // 객체반환
    return $this->_schema;
}
```