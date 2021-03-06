---
layout: page
title: "07 데이터 타입"
--- 
테이블에는 각각 데이터를 저장하기 위한 다수의 컬럼들을 같이 선언합니다. 컬럼을 선언 할 때는 컬럼의 데이터 타입도 같이 지정하게 됩니다. 데이터의 타입을 같이 지정하는 이 유는 테이블의 저장 공간을 효율적으로 사용하기 위해서입니다. 또한 빠른 접근과 처리를 위해서입니다.  

테이블의 컬럼에서 데이터 타입을 지정하는 것은 프로그램 언어에서 변수 타입을 지정하 는 것과 같은 의미입니다. 데이터의 타입은 입력되는 데이터의 종류에도 제한을 하게 됩 니다. 데이터 타입은 입력되는 자료의 신뢰성을 높여줍니다. 따라서 실수로 잘못된 데이 터를 입력하는 것을 방지합니다. 만일, 데이터 타입과 일치하는 유형의 자료를 입력하고 자 할 때는 DB시스템이 쿼리 실행 오류를 발생합니다.  

데이터 타입은 크게 네 가지로 구분할 수 있습니다. 

* 숫자형 
* 문자형 
* 날짜형 
* 그 외 

그중 가장 많이 사용하는 형식만 살펴봅니다. 

#### 07.1 [숫자형 데이터](07.1)
* 7.1.1 INT
* 07.1.2 TINYINT
* 07.1.3 SMALLINT
* 07.1.4 MEDIUMINT 
* 07.1.5 BIGINT
* 07.1.6 FLOAT
* 07.1.7 DOUBLE
* 07.1.8 DECIMAL

#### 07.2 [문자 자료형](07.2)
* 07.2.1 CHAR
* 07.2.2 VARCHAR
* 07.2.3 TEXT
* 07.2.4 LONGTEXT

#### 07.3 [날짜/시간 자료형](07.3)
* 07.3.1 DATETIME 
* 07.3.2 DATE
* 07.3.3 YEAR
* 07.3.4 TIME
* 07.3.5 TIMESTAMP