# 프리미티브 타입과 레퍼런스 타입

자바에는 프리미티브 타입과 레퍼런스 타입이 있습니다. 프리미티브 타입은 기본 데이터 타입이며, 레퍼런스 타입은 객체를 참조하는 타입이기 때문에 프리미티브 타입보다 연산 속도는 느리지만, 컬렉션 프레임워크에서 주로 사용됩니다.

### 프리미티브 타입

- **정수형**: `int`, `long`
- **부동소수형**: `float`, `double`

### 레퍼런스 타입

- **정수형 레퍼런스**: `Integer`, `Long`
- **부동소수형 레퍼런스**: `Float`, `Double`

### 컬렉션 프레임워크에서의 레퍼런스 타입 사용 예제

```java
import java.util.ArrayList; // ArrayList를 사용하기 위한 import
import java.util.Stack; // Stack을 사용하기 위한 import
import java.util.Queue; // Queue를 사용하기 위한 import
import java.util.ArrayDeque; // ArrayDeque를 사용하기 위한 import

public class Example {
    public static void main(String[] args) {
        // 정수형 레퍼런스를 저장하는 ArrayList 생성
        ArrayList<Integer> arrayList = new ArrayList<>();
        arrayList.add(1); // 정수 1 추가
        arrayList.add(2); // 정수 2 추가

        // 정수형 레퍼런스를 저장하는 Stack 생성
        Stack<Long> stack = new Stack<>();
        stack.push(100L); // Long형 정수 100 추가
        stack.push(200L); // Long형 정수 200 추가

        // 부동소수형 레퍼런스를 저장하는 Queue 생성
        Queue<Float> queue = new ArrayDeque<>();
        queue.add(3.14f); // Float형 숫자 3.14 추가
        queue.add(2.71f); // Float형 숫자 2.71 추가

        // 부동소수형 레퍼런스를 저장하는 ArrayDeque 생성
        ArrayDeque<Double> arrayDeque = new ArrayDeque<>();
        arrayDeque.add(1.618); // Double형 숫자 1.618 추가
        arrayDeque.add(2.718); // Double형 숫자 2.718 추가
    }
}
```

### 정수형

정수형은 양수, 음수, 0을 포함하며, 다양한 수학적 연산을 수행할 수 있습니다.

### 부동소수형

부동소수형은 소수점을 포함한 수를 저장하는 데 사용됩니다. 자바에서는 이진법으로 표현되기 때문에 오차가 발생할 수 있습니다. 이를 **엡실론**이라고 부르며, 아래 예제와 같이 표현할 수 있습니다.

```java
public class FloatingPointExample {
    public static void main(String[] args) {
        // 부동소수형 변수 선언
        double num1 = 0.1; // 0.1을 이진법으로 표현
        double num2 = 0.2; // 0.2를 이진법으로 표현
        double sum = num1 + num2; // 두 숫자의 합

        // 오차 확인
        System.out.println("Sum: " + sum); // 예상: 0.3, 실제: 0.30000000000000004
    }
}
```

### 부동소수형 비교하기

부동소수형 값들을 직접 비교할 경우 엡실론으로 인한 오차 때문에 예상과 다른 결과를 얻을 수 있습니다. 따라서 `Math.abs()`를 사용하여 오차 범위를 고려해야 합니다. 

```java
public class EpsilonComparison {
    public static void main(String[] args) {
        double num1 = 0.1 + 0.2; // 0.1과 0.2의 합
        double expected = 0.3; // 기대하는 결과
        double epsilon = 1e-10; // 허용 오차

        // 두 수를 비교
        if (Math.abs(num1 - expected) < epsilon) {
            System.out.println("결과는 예상한 값과 같습니다."); // 허용 오차 내에서 일치
        } else {
            System.out.println("결과는 예상한 값과 다릅니다."); // 허용 오차를 초과
        }
    }
}

```

이렇게 함으로써 부동소수형의 정확한 비교를 할 수 있습니다.
