# 2. 자바의 기본 문법 점검하기

## 조건문: if 문과 else 문

실행의 흐름을 바꿔 코드를 선택적으로 실행하는 방법을 제공

```java
public class Main {
    public static void main(String[] args) {
        int number = 1;

        if (number == 1) {
            System.out.println("if 블록입니다.");
        } else if (number == 2) {
            System.out.println("else if 블록입니다.");
        } else {
            System.out.println("else 블록입니다.");
        }
    }
}
```

## 반복문: for 문과 while 문

### for문

```java
public class Main {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5};

        for (int i = 0; i < array.length; i++) {
            System.out.println("i = " + array[i]);
        }
    }
}
```

### while문

```java
public class Main {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5};
        int i = 0;

        while (i < array.length) {
            System.out.println("i = "+ array[i]);
            i++;
        }
    }
}
```

## 다형성: 상속과 인터페이스

### 다형성(Polymorphism)

하나의 객체가 내부적으로 여러 타입을 가질 수 있고,

어떤 타입이 들어 있느냐에 따라 각기 다른 동작을 하는 성질

```java
public interface Car {}

public class Sonata implements Car {}

public class K5 implements Car {}

public class Main {
    public static void main(String[] args) {
        Car car1 = new Sonata();
        Car car2 = new K5();
    }
}
```

- Car → 인터페이스
- Sonata, K5 → 인터페이스를 구현하는 구현체(Implement)

→ 인터페이스(혹은 부모 클래스)의 참조 변수로 구현 클래스(혹은 자식 클래스)의 인스턴스를 넣어 사용할 수 있다.