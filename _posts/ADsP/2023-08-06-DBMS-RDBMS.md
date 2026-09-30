---
title: "[ADsP 1과목] DBMS와 RDBMS의 차이점"
categories:
  - Data
tags: [Data, ADsP]
---

## DBMS와 RDBMS

DBMS(Database Management System)는 데이터의 저장, 조회, 갱신 등을 관리하는 소프트웨어다. RDBMS(Relational Database Management System)는 관계형 데이터 모델을 사용하는 DBMS다. 두 개념은 서로 반대되는 것이 아니라 포함 관계에 있다.

관계형 데이터베이스는 데이터를 테이블의 행과 열로 표현하며, 키를 이용해 테이블 사이의 관계를 정의할 수 있다. 대표적인 RDBMS로 Oracle Database, MySQL, SQL Server 등이 있다.

## 비교할 때 주의할 점

- RDBMS도 DBMS의 한 종류다.
- 보안, 동시 사용자 수, 처리 가능한 데이터의 규모는 제품과 구성에 따라 달라진다.
- XML은 데이터를 표현하는 형식이며, 그 자체가 DBMS는 아니다.
- 파일에 저장된다는 이유만으로 데이터 사이에 관계가 없다고 단정할 수는 없다.

## 트랜잭션의 ACID

| 특성 | 의미 |
| --- | --- |
| 원자성(Atomicity) | 트랜잭션의 작업을 모두 수행하거나 모두 취소한다. |
| 일관성(Consistency) | 정의된 규칙과 제약을 만족하는 상태를 유지한다. |
| 격리성(Isolation) | 동시에 수행되는 트랜잭션의 간섭을 제어한다. |
| 지속성(Durability) | 커밋된 결과를 지속적으로 보존한다. |

## 참고

- [Oracle: Introduction to Oracle Database](https://docs.oracle.com/html/E25789_01/intro.htm)
