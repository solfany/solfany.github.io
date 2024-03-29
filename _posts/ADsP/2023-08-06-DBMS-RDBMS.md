---
title: "[ADsP 1과목] DBMS와 RDBMS의 차이점  "
categories:
  - Data
tags: [Data, ADsP]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
---

| DBMS                                                                                           | RDBMS                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DBMS는 데이터를 파일로 저장합니다.                                                             | RDBMS는 데이터를 테이블형식으로 저장합니다.                                                                                                                                                   |
| DBMS에서 데이터는 일반적으로 계층적 형식 또는 탐색 형식으로 저장됩니다.                        | RDBMS에서 테이블들은 primary key라는 식별자가 있으며데이터의 값들은 테이블 형식으로 저장됩니다.                                                                                               |
| DBMS에는 표준화라는것이 없습니다.                                                              | RDBMS는 표준화 되어있습니다.                                                                                                                                                                  |
| DBMS는 데이터보관에 있어 어떠한 보안도 제공하지 않습니다.                                      | RDBMS는 ACID를위한 무결성 제약을 정의합니다.( A - Atomocity 원자성  C - Consistency 일관성   I - Isolation 고립성  D - Durability  지속성 )ACID에 관련해서는 테이블 밑에 더보기를 눌러주세요. |
| DBMS는 데이터를 저장하기 위해 파일 시스템을 사용하고, 그렇기때문에 테이블간의 관계가 없습니다. | RDBMS시스템은 저장된 데이터에 접근하기 위해 데이터의 테이블 형식 구조를 지원합니다.                                                                                                           |
| DBMS는 적은 데이터를 처리하기에 좋습니다.                                                      | RDBMS는 많은 데이터를 처리하기 좋습니다.                                                                                                                                                      |
| DBMS를 예로들면 XML등이 있습니다.                                                              | RDBMS를 예로들면 mysql, oracle, sql server등이 있습니다.                                                                                                                                      |

    개인 공부 기록용 블로그입니다.
    본문에 오류가 포함되어 있을 수도 있습니다.
    댓글 또는 메일 주시면 수정하도록 하겠습니다.🍀

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
