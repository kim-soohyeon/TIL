# **배열과 ArrayList 차이점 및 활용 예시**

배열(Array)과 ArrayList는 자바에서 데이터를 저장하고 관리할 수 있는 중요한 자료구조입니다. 이 글에서는 배열과 ArrayList의 차이점을 비교하고 각각의 선언 방법과 활용법을 살펴보겠습니다.

### 배열이란?

배열은 인덱스와 값을 일대일 대응해 관리하는 정적 자료구조입니다. 배열은 임의 접근(Random Access) 방식을 사용하므로, 배열 내의 어느 위치에 있든 해당 값을 바로 조회할 수 있습니다.

### 배열의 선언 예시:

```java
// 선언과 동시에 초기화
int[] arr1 = {0, 1, 2, 3, 4};

// 크기만 선언하고 나중에 값 할당
int[] arr2 = new int[5];
arr2[0] = 1;
arr2[1] = 2;
```

### 배열과 ArrayList의 차이점

1. **크기 고정**: 배열은 선언할 때 크기가 고정됩니다. 즉, 한 번 크기를 설정하면 동적으로 늘어나거나 줄어들지 않습니다.
2. **동적 크기 조정**: ArrayList는 크기가 동적으로 조정될 수 있습니다. 필요에 따라 요소를 추가하거나 삭제하면 크기가 자동으로 변경됩니다.

### ArrayList란?

ArrayList는 크기가 동적으로 변경되는 배열입니다. 요소를 삽입하거나 삭제할 때마다 크기가 자동으로 조정되기 때문에, 데이터의 개수가 고정되지 않은 경우 유용하게 사용됩니다.

### ArrayList의 선언 및 활용 예시

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // ArrayList 선언
        ArrayList<Integer> arrayList = new ArrayList<>();

        // 데이터 추가
        arrayList.add(1);
        arrayList.add(2);
        arrayList.add(3);

        // 데이터 접근
        System.out.println("첫 번째 요소: " + arrayList.get(0));

        // 데이터 삭제
        arrayList.remove(1); // 두 번째 요소 삭제

        // ArrayList의 크기 확인
        System.out.println("ArrayList의 크기: " + arrayList.size());
    }
}
```

### 언제 배열을 사용하고 언제 ArrayList를 사용할까?

- **배열**: **데이터의 개수가 고정**되어 있고, **빠른 접근과 수정**이 필요한 경우 배열을 사용하는 것이 좋습니다. 배열은 메모리 상에서 연속적으로 저장되기 때문에 빠른 성능을 기대할 수 있습니다.
- **ArrayList**: **데이터의 개수가 유동적**이거나 **삽입, 삭제가 빈번**하게 일어날 때는 ArrayList가 더 유리합니다. ArrayList는 내부적으로 배열을 사용해 데이터를 관리하지만, 크기가 자동으로 조정된다는 점에서 배열과 차별화됩니다.
