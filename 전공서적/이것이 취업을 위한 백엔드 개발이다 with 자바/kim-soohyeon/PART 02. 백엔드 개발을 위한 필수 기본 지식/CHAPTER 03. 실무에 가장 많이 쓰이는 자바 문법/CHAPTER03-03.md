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