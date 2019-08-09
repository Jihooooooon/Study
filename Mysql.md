mysql 기본 쿼리문 정리
================================

+ 접속 방법
    - mysql -u id -p (pass)
    
+ 데이터베이스 조회
    - show databases;
    
+ 데이터베이스 사용
    - use database;

+ 데이터베이스 생성
    - create database 이름
    -CREATE TABLE dept (
  dept_no INT(11) unsigned NOT NULL,
  dept_name VARCHAR(32) NOT NULL,
  PRIMARY KEY (dept_no)
);
    - CREATE TABLE posts ( 
  id bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  subject varchar(255) NOT NULL,
  content mediumtext,
  created datetime,
  user_id int(10) unsigned NOT NULL,
  user_name varchar(32) NOT NULL,
  hit int(10) unsigned NOT NULL default '0',  
  PRIMARY KEY (id)
);
    
+ 데이터베이스 삭제
    - drop database 데이터베이스 이름
    
+ 비밀번호 변경
    - mysqladmin -u root password 새로운 비밀번호

+ 구조 보기
    - desc 테이블

+ 이름 변경
    - rename 테이블 a to b
    
+ 삭제
    - drop table 테이블
    
+ 조회
    - select * from table;
    - select * from table limit n; n개만 가져옴
    - select * from table limit n,m; n번째 부터 m개 가져옴
    - select count(*) from table
    
