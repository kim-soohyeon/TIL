# [Java] Collection Framework: TreeSet과 HashSet의 차이점 및 예제

Java에서 `TreeSet`과 `HashSet`은 모두 **Set** 인터페이스를 구현하는 클래스입니다. 두 클래스 모두 **중복된 요소를 허용하지 않으며**, 데이터를 집합 형태로 저장하는 데 사용됩니다. 

### 1. 정의

- **TreeSet**
: **이진 검색 트리(Red-Black Tree)**를 기반으로 구현되어 있으며, **자동으로 요소를 정렬**합니다. 따라서 TreeSet에 저장된 요소는 항상 **오름차순**으로 정렬됩니다. 또한, 커스텀 비교기를 제공하여 정렬 기준을 변경할 수 있습니다.
- **HashSet**
: **해시맵(HashMap)**을 기반으로 구현되어 있으며, 요소의 순서를 보장하지 않습니다. HashSet은 **데이터를 빠르게 검색**할 수 있는 구조로 되어 있습니다.

### 2. 차이점

`TreeSet`은 데이터가 자동으로 정렬되어야 할 때 유용하고, `HashSet`은 빠른 데이터 검색이 필요한 경우에 적합합니다. 

| 특징 | TreeSet | HashSet |
| --- | --- | --- |
| 정렬 여부 | 오름차순으로 자동 정렬 | 순서 없음 |
| 시간 복잡도 | O(log n) | O(1) (평균적으로) |
| Null 허용 여부 | Null 값을 허용하지 않음 | Null 값을 하나 허용 |
| 사용 목적 | 정렬된 데이터 저장 시 사용 | 빠른 검색이 필요할 때 사용 |

---

### TreeSet 정렬 예제

### 1. TreeSet 오름차순 정렬

- 예제 코드
    
    ```java
    import java.util.TreeSet;
    
    public class AscendingOrderExample {
        public static void main(String[] args) {
            // TreeSet 기본 생성자로 오름차순 정렬
            TreeSet<String> treeSet = new TreeSet<>();
    
            treeSet.add("Banana");
            treeSet.add("Apple");
            treeSet.add("Orange");
    
            System.out.println("TreeSet (오름차순): " + treeSet);
        }
    }
    
    ```
    
- 출력
    
    ```less
    TreeSet (오름차순): [Apple, Banana, Orange]
    ```
    

### 2. TreeSet 내림차순 정렬

- 예제 코드
    
    ```java
    import java.util.TreeSet;
    import java.util.Comparator;
    
    public class DescendingOrderExample {
        public static void main(String[] args) {
            // Comparator.reverseOrder()를 사용하여 내림차순 정렬
            TreeSet<String> treeSet = new TreeSet<>(Comparator.reverseOrder());
    
            treeSet.add("Banana");
            treeSet.add("Apple");
            treeSet.add("Orange");
    
            System.out.println("TreeSet (내림차순): " + treeSet);
        }
    }
    
    ```
    
- 출력
    
    ```less
    TreeSet (내림차순): [Orange, Banana, Apple]
    ```
