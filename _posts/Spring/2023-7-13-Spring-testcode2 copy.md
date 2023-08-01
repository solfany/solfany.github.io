---
title: "[Spring Boot]spring boot Mysql 연동하기"
categories:
  - Spring
tags: [Java]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

# spring boot Mysql 연동하기

application.yml

```java
server:
  port: 8081

# database 연동 설정
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    #    각자 PC에 만들어놓은 Database이름 작성
    url: jdbc:mysql://localhost:3306/logindb?serverTimezone=Asia/Seoul&characterEncoding=UTF-8
    #    mysql에 생성한 사용자 계정 정보 작성.
    username: user
    password: 1111
  thymeleaf:
    cache: false

  # spring data jpa 설정
  jpa:
    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
    open-in-view: false
    show-sql: true
    hibernate:
      ddl-auto: update
```

데이터 베이스를 만들고 데이터 베이스를 기반으로 YML 파일을 작성한다.

Entity

```java
package com.example.springbootloginmysql.member.entity;

import lombok.Getter;
import lombok.Setter;

import javax.persistence.*;

@Entity
@Setter
@Getter
@Table(name = "member_table")
public class MemberEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = true) //unique 제약 조건을 추가한다.
    private String memberEmail;

    @Column(nullable = true)
    private String memberPassword;

    @Column(nullable = true)
    private String memberName;
}
```

yml 파일에 지정한 db를 바탕으로 entity class를 작성해준다.
각 어노테이션을 활용하여 작성한 코드 기반으로 db table을 만들어준다.

> 해당 코드를 실행시키면 자동으로 테이블이 만들어진다.

![스크린샷 2023-08-01 오후 4.18.19.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f14f4ce6-8d80-4538-b58b-ea866d700e1c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-08-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4.18.19.png)

콘솔에 데이터베이스가 정상적으로 만들어졌음을 확인할 수 있다.

```java
select * from member_table;
```

위의 명령어를 mysql 워크벤치에 입력해보면

![스크린샷 2023-08-01 오후 4.21.24.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ff8c593-dee0-4e5b-9461-b12fce62c1a1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-08-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4.21.24.png)

위와 같이 비어있는 talble 이 의도한 바와 같이 생성된 것을 확인 할 수 있다.

`url: jdbc:mysql://localhost:3306/logindb?serverTimezone=Asia/Seoul&characterEncoding=UTF-8`
해당 url 로 데이터 베이스가 자동으로 생성 된다.

mysql db 생성

```sql
create datedase 데이터베이스이름;
create user 유저이름@localhost indentified by 1234;
grant all pricaileges on 데이터베이스이름.* to 유저이름@localhost;
```

```sql
use logindb;
create table test(
	col1 varchar(10));
select * from test;
```

1. **`USE logindb;`**: 이 명령어는 "logindb" 데이터베이스를 현재 세션에서 사용하도록 설정합니다. 이후의 모든 쿼리들은 "logindb" 데이터베이스에서 실행됩니다. 즉, "logindb" 데이터베이스가 현재 활성 데이터베이스가 된다.
2. **`CREATE TABLE test (col1 VARCHAR(10));`**: 이 명령어는 "test"라는 이름의 테이블을 "logindb" 데이터베이스에 생성합니다. 이 테이블은 하나의 컬럼 "col1"을 가지며, 해당 컬럼은 최대 길이가 10인 문자열 (VARCHAR) 데이터형을 갖는다.
3. **`SELECT * FROM test;`**: 이 명령어는 "test" 테이블의 모든 데이터를 조회하는 쿼리이다. 현재 "test" 테이블은 아무 데이터도 포함하지 않기 때문에 결과로는 아무 것도 표시되지 않을 수 있다.

총 정리하면, 위의 명령어들은 "logindb" 데이터베이스를 사용하여 "test"라는 이름의 테이블을 생성하고, 해당 테이블에는 하나의 컬럼 "col1"이 있으며, 그 안에는 아무 데이터도 없는 상태를 만들어 냅니다. 이후에 데이터를 추가하고 조회하려면 INSERT 문과 다른 SELECT 문을 사용하야 한다!
