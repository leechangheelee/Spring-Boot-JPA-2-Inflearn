## **다음으로**

![image](https://user-images.githubusercontent.com/79301439/181474295-0f9b5aa2-159d-436c-b381-6f9450f6c72e.png)

```java
package jpabook.jpashop.repository;

import jpabook.jpashop.domain.Member;
import org.springframework.stereotype.Repository;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import java.util.List;

@Repository
public class MemberRepositoryOld {

    @PersistenceContext
    private EntityManager em;

    public void save(Member member) {
        em.persist(member);
    }

    public Member findOne(Long id) {
        return em.find(Member.class, id);
    }

    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class)
                .getResultList();
    }

    public List<Member> findByName(String name) {
        return em.createQuery("select m from Member m where m.name = :name", Member.class)
                .setParameter("name", name)
                .getResultList();
    }
}
```

![image](https://user-images.githubusercontent.com/79301439/181474490-d57134e8-aec1-473f-9556-3574de49da8b.png)

```java
package jpabook.jpashop.repository;

import jpabook.jpashop.domain.Member;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.List;

public interface MemberRepository extends JpaRepository<Member, Long> {

    List<Member> findByName(String name);
}
```

![image](https://user-images.githubusercontent.com/79301439/181474643-bf5d6d60-37ce-44c0-9152-28d68ed6c413.png)
