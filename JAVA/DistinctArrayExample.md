# [Java] int 배열 중복 제거 후 Integer 배열로 반환하기 (Stream API 활용)

`Stream API`를 활용하여 `int[]` 배열에서 중복된 값을 제거한 후, 이를 `Integer[]` 배열로 변환하는 방법입니다.

### 예제 코드:

```java
import java.util.Arrays;
import java.util.stream.IntStream;

public class DistinctArray {

    public static Integer[] removeDuplicates(int[] inputArray) {
        return Arrays.stream(inputArray)         // 1. Arrays.stream()으로 IntStream 생성
                .distinct()                     // 2. 중복 제거
                .boxed()                        // 3. int형 값을 Integer로 변환
                .toArray(Integer[]::new);       // 4. Integer 배열로 변환
    }

    public static void main(String[] args) {
        int[] inputArray = {1, 2, 2, 3, 4, 4, 5};
        Integer[] result = removeDuplicates(inputArray);
        System.out.println(Arrays.toString(result));  // 결과 출력
    }
}
```

### 코드 설명:

1. **`Arrays.stream(inputArray)`**
    
    `int[]` 배열을 `IntStream`으로 변환하는 메서드입니다. `IntStream`은 기본형 `int` 데이터를 다루는 스트림입니다.
    
2. **`distinct()`**
    
    `IntStream`에서 중복된 값을 제거하는 메서드입니다. 이 메서드를 사용하면 배열 내의 중복 요소가 제거되고, 고유한 값들만 남습니다.
    
3. **`boxed()`**
    
    `IntStream`의 기본형 `int` 데이터를 참조형 `Integer`로 변환하는 메서드입니다. 기본형을 참조형으로 래핑해 객체로 취급할 수 있게 됩니다.
    
4. **`toArray(Integer[]::new)`**
    
    스트림의 결과를 배열로 변환하는 메서드입니다. `Integer[]::new`는 새로운 `Integer[]` 배열을 생성하기 위한 생성자 참조로 사용됩니다.
    

### 출력 결과:

```java
[1, 2, 3, 4, 5]
```

이 코드를 통해, `int[]` 배열의 중복 요소가 제거되고 `Integer[]` 배열로 변환된 결과를 얻을 수 있습니다.
