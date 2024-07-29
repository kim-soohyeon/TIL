# [Java] @RequiredArgsConstructor

- @RequiredArgsConstructor
    - 롬복(Lombok) 라이브러리에서 제공하는 애너테이션
    - final 키워드나 @NotNull이 붙은 필드를 생성자로 만들어줌
    - @RequiredArgsConstructor 예제
        
        `@RequiredArgsConstructor`를 사용하면, 클래스의 `final` 필드나 `@NotNull`이 붙은 필드를 매개변수로 받는 생성자를 자동으로 생성해줍니다.
        
        ```java
        import lombok.RequiredArgsConstructor;
        
        @RequiredArgsConstructor
        public class Person {
            private final String name;
            private final int age;
            @NotNull
            private String address;
        
            // 이 생성자가 롬복에 의해 자동으로 생성됩니다.
            // public Person(String name, int age, @NotNull String address) {
            //     this.name = name;
            //     this.age = age;
            //     this.address = address;
            // }
        }
        
        ```
        
        위 예제에서는 `@RequiredArgsConstructor` 애너테이션이 `name`, `age` 필드와 `address` 필드를 초기화하는 생성자를 자동으로 생성해줍니다. 이는 코드의 간결성과 가독성을 높이는 데 큰 도움이 됩니다.
        
    - 참고 개념
        - final 키워드란?
        `final` 키워드는 자바에서 변수, 메서드, 클래스에 사용할 수 있는 제한자입니다.
            - **변수에 사용**
            : `final` 키워드가 붙은 변수는 한 번 초기화되면 더 이상 값을 변경할 수 없습니다. 이는 상수를 선언할 때 주로 사용됩니다.
                
                ```java
                public class Example {
                    private final int number = 10;
                
                    public void changeNumber() {
                        // number = 20;  // 컴파일 에러 발생: final 변수는 값을 변경할 수 없음
                    }
                }
                
                ```
                
            - **메서드에 사용**
            : `final` 키워드가 붙은 메서드는 서브클래스에서 오버라이드할 수 없습니다.
                
                ```java
                public class Parent {
                    public final void show() {
                        System.out.println("This is a final method.");
                    }
                }
                
                public class Child extends Parent {
                    // public void show() {
                    //     // 컴파일 에러 발생: final 메서드는 오버라이드할 수 없음
                    // }
                }
                
                ```
                
            - **클래스에 사용**
            : `final` 키워드가 붙은 클래스는 서브클래스를 가질 수 없습니다. 즉, 상속이 불가능합니다.
                
                ```java
                public final class FinalClass {
                    // 클래스 내용
                }
                
                // public class SubClass extends FinalClass {
                //     // 컴파일 에러 발생: final 클래스는 상속할 수 없음
                // }
                
                ```
                
        - @NotNull 어노테이션이란?
        @NotNull이 붙은 필드는 반드시 초기화되어야 하며, null 값을 가질 수 없습니다.
            
            ```java
            public class Example {
                @NotNull
                private String name;
                
                public Example(@NotNull String name) {
                    this.name = name;
                }
                
                public void setName(@NotNull String name) {
                    this.name = name;
                }
                
                @NotNull
                public String getName() {
                    return name;
                }
            }
            
            ```
            
            위 예제에서는 `name` 필드, 생성자의 매개변수, 그리고 `getName` 메서드의 반환 값이 모두 `null`이 될 수 없음을 명시하고 있습니다.
            
        - 생성자란?
        생성자는 객체가 생성될 때 호출되는 특수한 메서드로, 객체의 초기 상태를 설정하는 데 사용됩니다. 생성자는 클래스 이름과 동일한 이름을 가지며, 반환 타입이 없습니다. 생성자는 매개변수를 가질 수 있으며, 이를 통해 객체를 생성할 때 필요한 초기값을 전달받을 수 있습니다.
            
            ```java
            public class Person {
                private String name;
                private int age;
            
                // 생성자
                public Person(String name, int age) {
                    this.name = name;
                    this.age = age;
                }
            
                // 기본 생성자
                public Person() {
                }
            
                // 기타 메서드
            }
            
            ```
            
            위 예제에서 `Person` 클래스는 두 개의 생성자를 가지고 있습니다. 하나는 `name`과 `age`를 초기화하는 생성자이고, 다른 하나는 매개변수가 없는 기본 생성자입니다.
