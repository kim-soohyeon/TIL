# 3. 자바 8 버전 이상의 모던한 자바 문법 다지기

# 자바 8 버전 이상이 필요한 이유

- 자바 8 버전의 주요 문법
    - 람다 표현식(Lambda Expression)
    - 스트림 API
    - Optional

## 람다 표현식

- 익명 함수(Anonymous function): 이름이 없는 함수

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List list = new ArrayList<String>();

        list.add("public");
        list.add("static");
        list.add("void");

        // 익명 클래스 코드
        list.sort(new Comparator<String>() {
            @Override
            public int compare(String str1, String str2) {
                return str1.compareTo(str2);
            }
        });

        // 람다 표현식 코드
        list.sort((Comparator<String>) (str1, str2) -> str1.compareTo(str2));
    }
}

```

### 파라미터 1개, 명령문 1개

파라미터가 1개일 때 파라미터를 감싸는 괄호 생략 가능

명령문이 1개일  때 함수를 감싸는 중괄호, 세미콜론 생략 가능

```java
var -> System.out.println(var1)
```

### 파라미터 1개, 명령문 2개 이상

명령문이 2개 이상일 때 중괄호로 명령문을 감싸야 한다.

```java
var -> {
	var1 = var1 + 1;
	System.out.println(var1);
	return var1;
}
```

### 파라미터 2개 이상, 명령문 1개

파라미터가 2개 이상일 때 괄호로 파라미터를 감싸야 한다.

```java
(var1, var2) -> System.our.println(var1 + var2)
```

### 파라미터 2개 이상, 명령문 2개 이상

파라미터는 괄호로 감싸고, 함수는 중괄호로 감싸야 한다.

```java
(var1, var2) -> {
	System.out.println(var1);
	System.out.println(var2);
}
```

## 스트림 API

### 스트림 API

: 컬렉션에 추가된 메서드의 집합

- 반복문을 스트림으로 변경하기
    
    ```java
    import java.util.ArrayList;
    import java.util.List;
    
    public class Main {
    
        public static void main(String[] args) {
            List list = new ArrayList<String>();
    
            list.add("public");
            list.add("static");
            list.add("void");
    
            list.stream().forEach(str -> System.out.println(str));
        }
    }
    
    ```
    

- 리스트에 1~10까지의 수를 넣고 2의 배수만 뽑는 예제
    
    ```java
    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.List;
    
    public class Main {
        public static void main(String[] args) {
            Integer[] integerArray = new Integer[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
            List<Integer> list = Arrays.asList(integerArray);
    
            List evenList = new ArrayList<Integer>();
    
            for (int i = 0; i < list.size(); i++) {
                Integer number = list.get(i);
                if (number % 2 == 0) { // 2로 나눴을 때의 나머지가 0이면 2의 배수이다.
                    evenList.add(number);
                }
            }
    
            for (int i = 0; i < evenList.size(); i++) {
                System.out.println(evenList.get(i));
            }
        }
    }
    
    ```
    
    - 스트림으로 변경
    
    ```java
    import java.util.Arrays;
    import java.util.List;
    import java.util.stream.Collectors;
    
    public class Main {
        public static void main(String[] args) {
            Integer[] integerArray = new Integer[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
            List<Integer> list = Arrays.asList(integerArray);
    
            List evenList = list.stream()
                    .filter(value -> value % 2 == 0).collect(Collectors.toList());
    
            evenList.stream().forEach(value -> System.out.println(value));
        }
    }
    
    ```
    

### forEach()

컬렉션의 요소들을 하나씩 꺼내어 반복한다.

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        Integer[] integerArray = new Integer[]{1, 2, 3, 4, 5};
        List<Integer> list = Arrays.asList(integerArray);
        list.stream().forEach(value -> System.out.println(value));
    }
}

```

### filter()

컬렉션의 요소들 중 조건에 맞는 요소만 뽑아 새로운 스트림을 만든다.

collect()와 함께 사용하면 조건을 만족하는 새로운 리스트를 만들 수 있다.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        Integer[] integerArray = new Integer[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        List<Integer> list = Arrays.asList(integerArray);
        List evenList = list.stream()
               .filter(value -> value % 2 == 0).collect(Collectors.toList());
        evenList.stream().forEach(value -> System.out.println(value));
    }
}

```

### distinct()

컬렉션의 요소에서 중복을 제거한다.

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        Integer[] integerArray = new Integer[]{1, 1, 1, 1, 2, 2, 2, 3, 3, 4};
        List<Integer> list = Arrays.asList(integerArray);
        List<Integer> distinctList = list.stream().distinct().toList();
        distinctList.stream().forEach(value -> System.out.println(value));
    }
}

```

### map()

컬렉션의 요소에 특정 연산을 적용하여 새로운 스트림을 만든다.

입력 컬렉션과 출력 컬렉션의 수는 동일하다.

- 소문자 요소를 대문자로 바꾸는 예제

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        String[] lowercaseArray = new String[]{"public", "static", "void"};
        List<String> lowercaseList = Arrays.asList(lowercaseArray);
        List<String> uppercaseList = lowercaseList.stream()
                .map(value -> value.toUpperCase()).toList();
        uppercaseList.stream().forEach(value -> System.out.println(value));
    }
}

```

### collect() / toList()

.collect(Collectors.toList()) 형태로 스트림을 간단하게 리스트로 만들 수 있다.

.toList()를 사용하여 간결하게 작성도 가능하다.

## Optional

### Optional

- NullPointException을 우아하게 해결하기 위해 등장함
    - cf. NullPointException
        
        : null이 들어 있는 레퍼런스 변수의 멤버(필드나 메서드)에 접근하려고할 때 발생하는 예외
        

```java
public class Main {
    private static String getSomeString() {
        return null; // 이 메서드는 항상 null을 반환한다.
    }

    public static void main(String[] args) {
        String isThisNull = getSomeString();

        if(null != isThisNull) {
            System.out.println(isThisNull.toUpperCase());
        }
    }
}

```

```java
public class Main {
    private static String getSomeString() {
        return null; // 이 메서드는 항상 null을 반환한다.
    }

    public static void main(String[] args) {
        String isThisNull = getSomeString();

        System.out.println(isThisNull.toUpperCase());
    }
}

```

Optional 활용하여 개선하기

```java
import java.util.Optional;

public class Main {
    private static Optional<String> getSomeString() {
        return Optional.empty(); // null을 반환하는 것이 아니라 비어 있는 Optional을 반환한다.
    }

    public static void main(String[] args) {
        Optional<String> isThisNull = getSomeString();

        isThisNull.ifPresent(str -> System.out.println(str.toUpperCase()));
    }
}

```

```java
import java.util.Optional;

public class Main {
    private static Optional<String> getSomeString() {
        return Optional.ofNullable("public static void");
    }

    public static void main(String[] args) {
        Optional<String> isThisNull = getSomeString();

        isThisNull.ifPresent(str -> System.out.println(str.toUpperCase())); // PUBLIC STATIC VOID가 출력된다.
    }
}

```

### 안티 패턴

Optional을 사용하면서 주의해야 할 패턴

- 디자인 패턴
    - S/W 개발 과정에서 자주 나타나는 문제 해결 방법 중 다른 분야에서도 재사용하기 좋은 코드의 패턴을 모아 이름을 붙인 것

- 안티 패턴
    - 디자인 패턴과 반대로 S/W 개발 과정에서 자주 나타나지만, 비효율적이거나 생산적이지 않은 패턴.
    - 가독성을 떨어뜨리거나 성능상 손실을 유발하므로 지양해야 함.
    - isPresent() 메서드를 마치 if 문처럼 잘못 사용한 예시
        
        ```java
        import java.util.Optional;
        
        public class Main {
            private static Optional<String> getSomeString() {
                return Optional.ofNullable("public static void");
            }
        
            public static void main(String[] args) {
                Optional<String> str = getSomeString();
        
                if(str.isPresent()) {
                    System.out.println(str.get().toUpperCase());
                }
            }
        }
        
        ```
        
    - Optional을 제대로 사용하는 코드로 변경한 예시
        
        ```java
        import java.util.Optional;
        
        public class Main {
            private static Optional<String> getSomeString() {
                return Optional.ofNullable("public static void");
            }
        
            public static void main(String[] args) {
                Optional<String> str = getSomeString();
        
                str.ifPresent((string) -> System.out.println(string.toUpperCase()));
            }
        }
        
        ```