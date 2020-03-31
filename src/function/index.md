---
layout: page
title: "함수"
--- 

# 함수
<hr>

MySQL은 쿼리 명령 이외에 데이터를 처리할 수 있는 다양한 함수를 제공하고 있습 니다. MySQL에서는 사용자 함수는 stored function(저장 함수)라고 부르기도 합니다.  

<br>

## 함수 만들기
<hr>

MySQL 5.0 이상 버전에는 사용자가 직접 함수를 생성하고 사용할 수 있는 기능을 제공 합니다. 

* [함수 생성](25.1)
    + 25.1.1 쿼리 실습
    + 25.2 함수 실행

* 25.2.1 [쿼리 실습](25.2)
    + 25.3 변수 선언 
    + 25.3.1 쿼리 실습

* 25.4 [함수 확인](25.3)
    + 25.4.1 쿼리 실습
    + 25.4.2 PHP 실습 

* 25.5 [함수 삭제](25.4)
    + 25.5.1 쿼리 실습
    + 25.5.2 PHP 실습

<br>

## 내장함수
<hr>

MySQL은 다양한 데이터 가공을 위해서 몇 가지 내장 함수를 제공합니다. 
내장 함수는 주로 Select 키워드와 함께 사용하지만 몇몇 함수들은 테이블 속성 값이나 검색 조건 값 등으로도 사용할 수 있습니다.  

내장 함수는 연산과 관련된 산술 함수, 문자열 함수, 날짜 시간 관련 함수 등이 있습니다.  

<br>

### 26.1 [산술 함수](26.1)
<hr>

* 26.1.1 AVG() 
* 26.1.2 COUNT( ) 
* 26.1.3 MAX( )
* 26.1.4 MIN( )
* 26.1.5 ROUND( )
* 26.1.6 SUM( ) 
* 26.1.7 ABS(숫자)
* 26.1.8 CEILING(숫자) 
* 26.1.9 FLOOR(숫자) 
* 26.1.10 TRUNCATE(숫자, 자릿수)  
* 26.1.11 GREATEST(숫자1, 숫자2, 숫자3 ...) 
* 26.1.12 LEAST(숫자1, 숫자2, 숫자3 ...)

<br>

### 26.2 [문자열 내장 함수](26.2)
<hr>

* 26.2.1 CONCAT( )
* 26.2.2 LEFT( )/RIGHT( )
* 26.2.3 LENGTH( ) 
* 26.2.4 공백 제거 함수 
* 26.2.5 SUBSTRING( )/MID( )
* 26.2.6 REPLACE( )
* 26.2.7 UPPER( )/UCASE( )
* 26.2.8 LCASE( )
* 26.2.9 REPEAT(문자, 반복 횟수)
* 26.2.10 REVERSE( )
* 26.2.11 ASCII(문자)
* 26.2.12 INSTR('문자열', '찾는 문자열')
* 26.2.13 IF(논리식, 참일 때 값, 거짓일 때 값)
* 26.2.14 IFNULL(값1, 값2) 

<br>

### 26.3 [SQL 날짜 함수](26.3)
<hr>

* 26.3.1 NOW(), SYSDATE( ), CURRENT_TIMESTAMP( )
* 26.3.2 CURDATE( ) 
* 26.3.3 CURTIME( )
* 26.3.4 DATE_ADD(날짜, INTERVAL 기준 값)
* 26.3.5 DATE_SUB(날짜, INTERVAL 기준 값)
* 26.3.6 YEAR(날짜), MONTH(날짜), DAY(날짜)
* 26.3.7 HOUR( ), MINUTE( ), SECOND( )
* 26.3.8 MONTHNAME(날짜), DAYNAME(날짜) 
* 26.3.9 DAYOFMONTH(날짜) 
* 26.3.10 DAYOFWEEK(날짜) 
* 26.3.11 WEEKDAY(날짜)
* 26.3.12 QUARTER(날짜)
* 26.3.13 DAYOFYEAR(날짜)
* 26.3.14 WEEK(날짜)
* 26.3.15 FROM_DAYS(날 수)
* 26.3.16 TO_DAYS(날짜)
* 26.3.17 DATE_FORMAT(날짜, '형식') 
* 26.3.18 TIME_FORMAT(날짜, '형식') 
* 26.3.19 TIME_TO_SEC(시간) 
* 26.3.20 SEC_TO_TIME(N) 

<br>

### 26.4 [수학 함수](26.4)
<hr>

* 26.4.1 PI( ) 
* 26.4.2 POW(X,Y) or POWER(X,Y) 
* 26.4.3 MOD(분자, 분모)
* 26.4.4 SQRT(X)
* 26.4.5 TAN(X)
* 26.4.6 SIN(X)
* 26.4.7 SIGN(X)
* 26.4.8 COT(X)
* 26.4.9 COS(X)
* 26.4.10 ATAN(X)
* 26.4.11 ATAN(Y,X), ATAN2(Y,X)
* 26.4.12 ACOS(X)
* 26.4.13 ASIN(X)
* 26.4.14 RADIANS(X) 
* 26.4.15 LOG10(X) 
* 26.4.16 LOG2(X)
* 26.4.17 LOG(X), LOG(B,X)
* 26.4.18 LN(X) 
* 26.4.19 FORMAT(X,D)
* 26.4.20 EXP(X) 
* 26.4.21 DEGREES(X) 
* 26.4.22 CRC32(expr)
* 26.4.23 RAND(), RAND(N).

<br>

### 26.5 [기타](26.5)
<hr>

* 26.5.1 VERSION( )
* 26.5.2 DATABASE( )
* 26.5.3 USER( )
* 26.5.4 CHARSET(문자열)

<br><br>