---
title: "[Spring Boot] LazyInitializationException 오류 "
categories:
  - Spring
tags: [Java, Spring, MVC 패턴]
toc_sticky: true
toc_label: "목록"
toc_icon: "bars"
toc_icon: "bars"
comments: true
---

![Untitled](https://tecoble.techcourse.co.kr/static/f11e41fcb46e962e898e8816ba02d5f5/6050d/spring.png)

### **발생한 오류**

LazyInitializationException

### **오류 메시지**

<aside style="background-color: #f7dce0; font-size: 0.6rem; border: 1px solid #000; padding: 10px; border-radius: 5px;">

org.hibernate.LazyInitializationException: failed to lazily initialize a collection of role: com.api.teamfresh.entity.Customer.keepers: could not initialize proxy - no Session

</aside>

**관련 코드**:

```java
VOC voc = vocService.findById(id);
```

**원인**:
이 오류는 Hibernate에서 엔터티의 속성이 지연 로딩(Lazy Loading)으로 설정되어 있을 때, 세션이 닫힌 후에 해당 속성에 접근하려고 할 때 발생한다.
여기서는 **`VOC`** 엔터티 내의 **`Customer`** 의 **`keepers`** 속성이 지연 로딩되어 있으며, 해당 속성에 접근하려 할 때 Hibernate 세션이 이미 종료되어 있어 발생하게 된다..

**해결 방법**:

1.  **`@Transactional` 사용** : Service 메소드에서 **`@Transactional`** 어노테이션을 사용하여 해당 메소드가 트랜잭션 범위 내에서 실행되게 한다.
    이렇게 하면 해당 메소드 내에서 지연 로딩을 사용하여 연관된 데이터를 가져올 수 있다.

    ```java
    @Transactional
    public VOC findById(Long id) {
    return vocRepository.findById(id).orElse(null);
    }
    ```

<br/>

2.  **명시적 초기화**: Hibernate의 **`initialize`** 메소드를 사용하여 지연 로딩된 속성을 명시적으로 초기화할 수 있습니다. 이 방법은 지연 로딩된 객체가 실제로 필요한 경우에만 사용해야 한다.

    ```java
    VOC voc = vocRepository.findById(id).orElse(null);
    if(voc != null) {
      Hibernate.initialize(voc.getCustomer().getKeepers());
    }
    ```
