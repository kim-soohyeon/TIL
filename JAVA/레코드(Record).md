# 레코드(Record)

- Java 14에서 처음 소개되었고, Java 16에서 정식 기능으로 추가되었습니다.
- 데이터 전달 객체(Data Transfer Object, DTO)를 더욱 간편하게 만들기 위한 기능을 제공합니다.
- 파라미터에 정의한 필드는 private final로 정의됩니다.
    - private
    → 클래스 외부에서 직접 접근 불가. 
    → 게터(getter)를 자동으로 생성함.
    - final
    → 초기화된 이후 값이 변경되지 않음(불변성)
    → 상속할 수 없음.
- 게터(getter)를 자동으로 만들기 때문에 따로 정의하지 않아도 됩니다.
    - 생성자, 게터, equals(), hashCode(), toString() 메서드를 자동으로 생성함.
    - 'get' 접두사 없이 필드명과 동일하게 자동 생성됨.

```java
record Person(String name, int age) {
    // 기본 생성자 외에 추가 로직을 포함할 수 있는 생성자
    public Person {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }

    // 추가 메서드 정의 가능
    public String greet() {
        return "Hello, my name is " + name + " and I am " + age + " years old.";
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person("Soohyeon", 20);

        // 필드는 private final로 정의되므로 직접 접근 불가
//         person.name = "Hyeonsoo"; // 컴파일 에러: final 필드이므로 값 변경 불가
//         System.out.println(person.name); // 컴파일 에러: private 필드에 직접 접근 불가

        // 게터 메서드를 통해 필드에 접근 (게터 메서드는 자동으로 생성됨)
        System.out.println(person.name()); // Soohyeon
        System.out.println(person.age());  // 20
        System.out.println(person.greet()); // Hello, my name is Soohyeon and I am 20 years old.
    }
}

```
