# JUnit과 AssertJ를 활용한 효과적인 단위 테스트 작성 방법

JUnit의 기본 개념과 Given-When-Then 패턴, JUnit 테스트 생명주기, 그리고 AssertJ를 활용하여 테스트 코드의 가독성을 높이는 방법에 대해 설명하겠습니다.

### JUnit

JUnit은 자바 기반의 단위 테스트를 위한 강력한 프레임워크입니다. 단위 테스트는 개별 구성 요소나 함수가 의도한 대로 동작하는지 확인하는 과정으로, JUnit은 이러한 테스트를 간편하고 효율적으로 작성할 수 있게 해줍니다.

### Given-When-Then 테스트 방식

JUnit에서 자주 사용되는 테스트 방식 중 하나는 Given-When-Then 패턴입니다. 이 패턴은 테스트를 보다 명확하고 읽기 쉽게 만들어줍니다. 각 단계는 다음과 같습니다.

- **Given**: 테스트의 초기 상태를 설정합니다. 필요한 객체를 생성하거나 초기화하는 작업을 포함합니다.
- **When**: 테스트하려는 동작을 실행합니다. 일반적으로 특정 메서드를 호출하거나 기능을 실행합니다.
- **Then**: 테스트 결과를 검증합니다. 예상한 결과와 실제 결과를 비교하여 테스트가 성공했는지 확인합니다.

예시 코드는 다음과 같습니다.

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.ResultActions;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@SpringBootTest
@AutoConfigureMockMvc
class Main {

    @Autowired
    protected MockMvc mockMvc;

    @Autowired
    private WebApplicationContext context;

    @BeforeEach
    public void mockMvcSetUp(){
        this.mockMvc = MockMvcBuilders.webAppContextSetup(context)
                .build();
    }

    @DisplayName("test(): GET /test?no=1 이면 응답 코드는 201, 응답 본문은 Created!를 리턴한다.")
    @Test
    public void getQuiz1() throws Exception {
        //given
        final String url = "/tesst";

        //when
        final ResultActions result = mockMvc.perform(get(url)
                .param("no", "1"));

        //then
        result
                .andExpect(status().isCreated())
                .andExpect(content().string("Created!"));
    }

}
```

### JUnit 테스트 생명주기

JUnit의 테스트 생명주기는 다음과 같은 어노테이션을 사용하여 관리됩니다:

- **@BeforeAll**: 모든 테스트가 실행되기 전에 한 번 실행됩니다. 주로 클래스 레벨의 초기 설정에 사용됩니다.
- **@BeforeEach**: 각 테스트 메서드가 실행되기 전에 실행됩니다. 테스트 메서드마다 새로운 상태를 설정하는 데 유용합니다.
- **@Test**: 실제 테스트 메서드를 나타내며, 각 테스트는 이 어노테이션을 통해 정의됩니다.
- **@AfterEach**: 각 테스트 메서드가 실행된 후에 실행됩니다. 테스트 후에 필요한 정리 작업을 수행합니다.
- **@AfterAll**: 모든 테스트가 실행된 후 한 번 실행됩니다. 주로 클래스 레벨의 정리 작업에 사용됩니다.

예시 코드는 다음과 같습니다.

```java
import org.junit.jupiter.api.*;

public class JUnitCycleTest {
    @BeforeAll
    static void beforeAll(){
        System.out.println("@BeforeAll");
    }

    @BeforeEach
    public void beforeEach(){
        System.out.println("@BeforeEach");
    }

    @Test
    public void test1(){
        System.out.println("test1");
    }

    @Test
    public void test2(){
        System.out.println("test2");
    }

    @AfterAll
    static void afterAll(){
        System.out.println("@AfterAll");
    }

    @AfterEach
    public void afterEach(){
        System.out.println("@AfterEach");
    }
}
```

콘솔 출력 결과는 다음과 같습니다.

```
@BeforeAll
@BeforeEach
test1
@AfterEach
@BeforeEach
test2
@AfterEach
@AfterAll
```

### AssertJ

JUnit과 함께 자주 사용되는 라이브러리 중 하나는 AssertJ입니다. AssertJ는 테스트 검증 문장을 보다 가독성 높고 유연하게 작성할 수 있게 해주는 라이브러리입니다. AssertJ를 사용하면 다음과 같이 더 읽기 쉬운 검증 문장을 작성할 수 있습니다:

```java
import org.junit.jupiter.api.Test;

import static org.assertj.core.api.AssertionsForClassTypes.assertThat;

public class JUnitAssertSample {
    @Test
    public void junitStringTest(){
        String name1 = "김수현";
        String name2 = "김수현";
        String name3 = "김길동";

        // 모든 변수가 null이 아닌지 확인
        assertThat(name1).isNotNull();
        assertThat(name2).isNotNull();
        assertThat(name3).isNotNull();

        // name1과 name2가 같은지 확인
        assertThat(name1).isEqualTo(name2);

        // name1과 name3이 다른지 확인
        assertThat(name1).isNotEqualTo(name3);
    }

    @Test
    public void junitIntTest(){
        int number1 = 20;
        int number2 = 0;
        int number3 = -50;
        
        //number1은 양수인지 확인
        assertThat(number1).isPositive();
        //number2은 0인지 확인
        assertThat(number2).isZero();
        //number3은 음수인지 확인
        assertThat(number3).isNegative();
        //number1은 number2보다 큰지 확인
        assertThat(number1).isGreaterThan(number2);
        //number3은 number2보다 작은지 확인
        assertThat(number3).isLessThan(number2);
    }
}

```

AssertJ는 다양한 검증 메서드를 제공하여 복잡한 조건을 쉽게 확인할 수 있게 해줍니다. 예를 들어, 컬렉션, 예외, 문자열 등의 다양한 검증을 간편하게 수행할 수 있습니다.

JUnit과 AssertJ를 함께 사용하면 단위 테스트를 보다 명확하고 간결하게 작성할 수 있어, 유지 보수성과 확장성이 높은 테스트 코드를 작성할 수 있습니다.
