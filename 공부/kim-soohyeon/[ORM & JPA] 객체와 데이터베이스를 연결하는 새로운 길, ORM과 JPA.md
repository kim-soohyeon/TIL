# [ORM & JPA] 객체와 데이터베이스를 연결하는 새로운 길, ORM과 JPA

ORM(Object-Relational Mapping)은 자바의 객체와 데이터베이스를 연결하는 혁신적인 프로그래밍 기법입니다. 이 기법을 통해 SQL을 몰라도 데이터베이스 값을 객체처럼 다룰 수 있어 자바로 간편하게 데이터를 추출할 수 있습니다.

### ORM의 장점

1. **SQL 미사용**: SQL을 직접 작성하지 않고도 데이터베이스에 접근할 수 있습니다.
2. **객체지향적 코드 작성**: 객체지향적으로 코드를 작성하여 비즈니스 로직에 집중할 수 있습니다.
3. **데이터베이스 시스템 추상화**: 데이터베이스 시스템이 추상화되어 있어 MySQL에서 PostgreSQL로의 전환 시 추가 작업이 거의 없습니다. 따라서 데이터베이스 시스템에 대한 종속성이 줄어듭니다.
4. **명확한 매핑 정보**: 매핑 정보가 명확하여 ERD에 대한 의존도를 낮출 수 있고 유지보수에 용이합니다.

### ORM의 단점

1. **복잡성 증가**: 프로젝트가 복잡해질수록 ORM의 사용이 어려워집니다.
2. **복잡한 쿼리의 한계**: 복잡하고 무거운 쿼리는 해결이 어려울 수 있습니다.

### JPA(Java Persistence API) 소개와 예시

JPA는 ORM 기술의 한 종류로, 자바 언어를 사용하여 객체와 데이터베이스를 매핑하고 상호 작용하는 데 사용됩니다. 아래는 간단한 JPA 예시입니다.

```java
import javax.persistence.*;

// Employee 엔티티 클래스 선언, 데이터베이스의 employees 테이블과 매핑
@Entity
@Table(name = "employees")
public class Employee {
    // id 필드를 기본키로 사용하며 자동으로 생성되도록 설정
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name; // 이름 필드
    private String position; // 직책 필드

    // Getters and setters 메서드
}

// Spring Data JPA의 Repository 인터페이스, Employee 엔티티와 관련된 데이터 액세스 메서드를 제공
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}

// Employee 객체를 다루는 REST API 컨트롤러
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/employees")
public class EmployeeController {
    @Autowired
    private EmployeeRepository employeeRepository; // EmployeeRepository 의존성 주입

    // POST 요청을 처리하여 새 직원 정보를 데이터베이스에 저장하고 저장된 직원 정보를 반환
    @PostMapping
    public Employee addEmployee(@RequestBody Employee employee) {
        return employeeRepository.save(employee); // 저장된 직원 정보 반환
    }

    // GET 요청을 처리하여 주어진 ID에 해당하는 직원 정보를 데이터베이스에서 조회하여 반환
    @GetMapping("/{id}")
    public Employee getEmployee(@PathVariable Long id) {
        return employeeRepository.findById(id).orElse(null); // 주어진 ID에 해당하는 직원 정보 반환, 없으면 null 반환
    }
}

```

위의 예시에서는 JPA를 사용하여 Employee 객체를 데이터베이스에 저장하고 검색하는 기능을 구현한 것을 볼 수 있습니다.

이처럼 JPA를 통해 SQL을 직접 작성하지 않고도 자바 코드로 데이터베이스와 상호 작용할 수 있습니다.
