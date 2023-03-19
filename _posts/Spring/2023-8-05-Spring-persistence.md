---
title: "[Spring Boot] JPA 영속성 "
categories:
  - Spring
tags: [Java, Spring]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

## 영속성이란?

데이터를 생성한 프로그램이 종료되어도 사라지지 않는 데이터의 특성을 말한다.

영속성을 갖지 않으면 데이터는 메모리에서만 존재하게 되고 프로그램이 종료되면 해당 데이터는 모두 사라지게 된다.

그래서 우리는 데이터를 파일이나 DB에 영구 저장함으로써 데이터에 영속성을 부여한다.

## JPA에서의 영속성

JPA의 핵심 내용은 엔티티가 영속성 컨텍스트에 포함되어 있냐 아니냐로 갈린다.
JPA의 엔티티 매니저가 활성화된 상태로 트랜잭션(@Transactional) 안에서 DB에서 데이터를 가져오면 이 데이터는 영속성 컨텍스트가 유지된 상태이다.
이 상태에서 해당 데이터 값을 변경하면 트랜잭션이 끝나는 시적에 해당 테이블에 변경 내용을 반영하게 된다.
따라서 우리는 엔티티 객체의 필드 값만 변경해주면 별도로 update()쿼리를 날릴 필요가 없게 된다! 이 개념을 더티 체킹이라고 한다.

## 영속성 컨텍스트란?

위에서도 말했다시피 영속성 컨텍스트(persistence context) 는 '엔티티를 영구 저장하는 환경' 이라는 뜻이다. EntityManager 를 이용해 Entity 를 저장하거나 조회할 때 EntityManager 는 영속성 컨텍스트에 Entity 를 보관하고 관리한다.
EntityManger객체.persist(Entity객체) 를 실행하면 영속성 컨텍스트가 Entity 를 관리하게 된다.
영속성 컨텍스트는 눈에 보이지 않는 논리적인 개념이다.
또한 EntityManager 를 하나 생성할 때 하나가 만들어지며, EntityManager 를 통해 접근할 수 있고 관리할 수 있다.

<br>

**영속성 컨텍스트의 특징은 아래와 같다!**

### 영속성 컨텍스트는 Entity 를 식별자 값으로 구분한다.

Entity에서 @Id 어노테이션을 통해 지정한 멤버변수가 영속성 컨텍스트에 식별자 값으로 저장된다.

JPA 는 보통 트랜잭션을 커밋하는 순간 영속성 컨텍스트에 새로 저장된 Entity를 데이터베이스에 반영한다.(이런 과정을 flush라 한다.)

### 1차 캐시를 이용한다.

영속성 컨텍스트 내부에 존재하는 캐시(Map)를 1차 캐시라 한다. 영속 상태의 Entity는 모두 이곳에 저장되며 키는 @Id 로 매핑한 식별자이며 값은 Entity 인스턴스이다. entityManager.find() 메소드를 호출하면 먼저 1차 캐시에서 Entity를 찾고, 만약 찾는 Entity 가 1차 캐시에 없으면 데이터베이스에서 조회한 후 1차 캐시에 저장하고 영속 상태인 해당 객체를 반환한다.

또한 객체의 동일성을 보장한다.

```java
Person hyeona = new Person(1, "hyeona"); // id, name

entityManager.persist(hyeona);

Person hyeona1 = entityManager.find(Person.class, 1);

Person hyeona2 = entityManager.find(Person.class, 1);

hyeona1 == hyeona2 // true
```

이와 같이 1차 캐시에 있는 같은 Entity 인스턴스를 반환하기 때문에 Entity의 동일성을 보장한다.

### 트랜잭션을 지원하는 쓰기 지연을 수행한다.

EntityManager 는 트랜잭션을 commit 하기 직전까지 데이터베이스에 Entity 를 저장하지 않고 영속성 컨텍스트 내부의 SQL 저장소에 생성 쿼리를 저장해둔다.
이 후 commit 을 하게 되면 저장해두었던 쿼리를 데이터베이스에 보낸다.
이것을 트랜잭션을 지원하는 쓰기 지연이라고 한다.

트랜잭션을 commit 하면 EntityManager 는 영속성 컨텍스트를 flush() 한다.
flush() 란 영속성 컨텍스트의 변경 내용을 데이터베이스에 동기화하는 작업으로 등록, 수정, 삭제한 Entity 를 데이터베이스에 반영한다.
즉, 쓰기 지연 SQL 저장소에 모인 쿼리를 데이터베이스에 보낸다.
이러한 동기화 작업을 거친 후 실제 데이터베이스 트랜잭션을 commit 한다.

### 변경을 감지한다.

영속성 컨텍스트에는 이전 flush() 때의 Entity 상태를 복사해서 저장해둔 스냅샷이 존재한다.
JPA는 flush() 시점에 스냅샷과 Entity를 비교해 변경된 Entity를 찾는다.
만약 있다면 각각의 객체에 대한 수정 쿼리를 만들어 쓰기 지연 SQL 저장소에 저장한 후 한꺼번에 데이터베이스로 보내고 데이터베이스 트랜잭션을 commit 하게 된다.

여기서 수정 쿼리는 Entity의 모든 필드를 업데이트한다.
이렇게 하면 수정 쿼리를 애플리케이션 로딩 시점에 미리 생성해두고 재사용할 수 있으며, 데이터베이스에 동일한 쿼리를 보낼 때 데이터베이스가 이전에 한 번 파싱된 쿼리를 재사용하기 때문에 성능상 장점이 된다.

변경 감지는 영속성 컨텍스트가 관리하는 영속 상태의 엔티티에만 적용된다.
바꿔 말하면, 준영속 상태의 객체는 아무리 수정해도 영속성 컨텍스트가 변경을 감지하지 못한다.

### 지연 로딩을 수행한다.

지연 로딩(Lazy Loading) 이란 실제 객체 대신 프록시 객체를 로딩해두고 해당 객체를 실제 사용할 때 영속성 컨텍스트를 통해 데이터를 불러오는 방법이다.

![img](https://velog.velcdn.com/images%2Fdevtel%2Fpost%2Fa9b7dd3e-df6d-4a27-b8fd-9337a208a9ce%2FUntitled%209.png)

memberDAO.find(memberId)에서는 Member 객체에 대한 SELECT 쿼리만 날린다.
Team team = member.getTeam()로 Team 객체를 가져온 후에 team.getName()처럼 실제로 team 객체를 건드릴 때!
즉, 값이 실제로 필요한 시점에 JPA가 Team에 대한 SELECT 쿼리를 날린다.
Member와 Team 객체 각각 따로 조회하기 때문에 네트워크를 2번 타게 된다.
Member를 사용하는 경우에 대부분 Team도 같이 필요하다면 즉시 로딩을 사용한다.
