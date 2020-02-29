# 09 속성 
테이블은 컬럼 데이터형 타입과 별개로 제약사항 속성을 추가할 수 있습니다. 추가된 제 약사항 속성은 컬럼의 데이터를 처리하는 데 별도의 규칙이 적용됩니다.  

컬럼의 제약사항 속성은 반드시 사용해야 하는 것은 아닙니다. 옵션과 같은 성격을 띕니다. 
속성을 설정하게 되면 데이터의 무결성을 보완하고 테이블의 데이터 검색 속도 개 선 등의 이점이 있습니다.   

테이블을 생성할 때 기본적으로 많이 사용하는 Primary Key, Auto Increament 등 몇 가지의 속성이 있습니다. 
제약사항 속성은 CREATE TABLE 명령을 통하여 테이블을 생 성할 때 함께 설정합니다. 또는 ALTER TABLE 명령을 통하여 나중에 추가할 수 있습 니다.  

| 쿼리 문법 | 
```sql
CREATE TABLE table_name (
     column1 datatype constraint,
     column2 datatype constraint,
     column3 datatype constraint,
    ....
);
```

제약사항(constraint)은 컬럼의 데이터 타입 설정 뒤에 위치합니다. 
MySQL은 일곱 가지의 제약사항 속성을 지원합니다.  

* NOT NULL : 컬럼 필드의 NULL 입력을 허용/방지합니다. 
* UNIQUE: 중복값 입력을 방지합니다. 
* PRIMARY KE: NOT NULL 과 UNIQUE 결합된 기본 데이터 키입니다. 
* FOREIGN KEY : 다른 테이블의 값을 참조하여 연결합니다. 
* CHECK: 데이터 입력 유효성을 설정합니다. 
* DEFAULT: 컬럼 필드의 초기값을 설정합니다. 
* INDEX: 빠른 접근을 위한 인덱스입니다. 

#### 09.1 제약사항 [NOT NULL](09/1)
* 09.1.1 쿼리 실습 
* 09.1.2 PHP 실습  

#### 09.2 [기본값 속성](09/2) - DEFAULT
* 09.2.1 쿼리 실습
* 09.2.2 PHP 실습 

#### 09.3 [유일값](09/3)  - UNIQUE
* 09.3.1 쿼리 실습 
* 09.3.2 PHP 실습 

#### 09.4 [프라이머리 키](09/4) - PRIMARY KEY
* 09.4.1 쿼리 실습 

#### 09.5 [CHECK](09/5)  
* 09.5.1 쿼리 실습 

#### 09.6 [자동 증가](09/6) - AUTO INCREMENT 
* 09.6.1 쿼리 실습
* 09.6.2 PHP 실습 

#### 09.7 [색인](09/7) - INDEX
* 09.7.1 색인 생성
* 09.7.2 색인 확인
* 09.7.3 색인 삭제

#### 09.8 [외래 키](09/8) - FOREIGN KEY
* 09.8.1 외래 키 설정
* 09.8.2 외래 키 수정
* 09.8.3 외래 키 삭제