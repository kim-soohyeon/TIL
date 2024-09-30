### 자바에서 문자열과 이뮤터블(Immutable) 객체

- **이뮤터블 객체(Immutable Object)**
    - 한 번 생성되면 내부 상태를 변경할 수 없는 객체를 의미하며표적인 이뮤터블 객체로는 `String`이 있습니다.
- **뮤터블 객체(Mutable Object)**
    - 생성된 후에도 값을 변경할 수 있는 객체를 말합니다.

### 이뮤터블 객체와 시간 복잡도

자바의 `String` 클래스는 이뮤터블하기 때문에 문자열을 변경하려고 하면 항상 새로운 문자열 객체를 생성합니다.

```java
String str = "Hello";
str = str + " World";
```

위 코드는 `str`에 `"Hello World"`라는 값을 할당하지만, 내부적으로는 새로운 `String` 객체가 생성되어 메모리에 저장됩니다. 

즉, 문자열을 변경할 때마다 새로운 객체가 생성되므로, 메모리 사용량이 증가할 수 있으며, 이는 특히 반복적인 문자열 조작이 있을 때 성능에 부정적인 영향을 미칠 수 있습니다. 

시간 복잡도 측면에서는 문자열을 계속 연결할 경우 O(n)으로, 매번 새로운 객체를 만드는 과정이 추가되므로 효율적이지 않습니다.

### StringBuilder와 StringBuffer

이러한 문제를 해결하기 위해 자바는 **뮤터블 객체**인 `StringBuilder`와 `StringBuffer`를 제공합니다. 이 둘은 문자열을 변경할 때 새로운 객체를 만들지 않고, 기존 객체의 내부 값을 변경하기 때문에 메모리 및 성능 측면에서 훨씬 효율적입니다.

- **StringBuffer**
: **thread-safe**합니다. 즉, 여러 스레드가 동시에 이 객체에 접근해도 안전하게 동작할 수 있습니다. 이를 위해 내부적으로 **동기화(synchronized)** 처리가 되어 있어, 멀티스레드 환경에서 안전하지만, 이 동기화 처리로 인해 성능이 다소 느릴 수 있습니다.
- **StringBuilder**
: **thread-safe**하지 않습니다. 동기화 처리가 없기 때문에 멀티스레드 환경에서는 안전하지 않지만, **단일 스레드** 환경에서는 불필요한 동기화 오버헤드가 없어서 `StringBuffer`보다 더 빠르게 동작합니다.

따라서, **단일 스레드** 환경에서는 `StringBuilder`를 사용하고, **멀티스레드** 환경에서는 안전한 `StringBuffer`를 사용하는 것이 좋습니다.

### StringBuilder 사용법 예

다음은 `StringBuilder`를 사용한 문자열 조작의 간단한 예입니다.

```java
public class Main {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");

        sb.append(" World");
        sb.append("!");

        System.out.println(sb.toString());  // 출력: Hello World!
    }
}
```

 `StringBuilder`는 내부 문자열을 변경하며 새로운 객체를 생성하지 않습니다. `append()` 메서드를 사용하여 문자열을 이어 붙일 수 있습니다.

