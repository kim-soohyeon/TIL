# 큐(Queue): 개념과 ADT 정의, 그리고 활용법 (Java 예제포함)
## **큐의 개념**

큐**(Queue)**는 ‘줄을 서다’라는 뜻을 가지며, **먼저 들어간 데이터가 먼저 나오는 자료 구조**입니다. 이러한 특징을 **선입선출(FIFO, First In First Out)**이라고 합니다. 큐에서 삽입하는 연산을 **Enqueue(Add)**, 꺼내는 연산을 **Dequeue(Poll)**이라고 합니다.

---

## **큐의 정의**

### **큐의 ADT(Abstract Data Type, 추상 자료형)**

| **메서드** | **설명** |
| --- | --- |
| **`boolean isFull()`** | 큐의 데이터 개수가 최대 크기(**`maxsize`**)인지 확인합니다. 가득 차 있다면 **`true`**, 아니면 **`false`**를 반환합니다. |
| **`boolean isEmpty()`** | 큐에 데이터가 하나도 없는지 확인합니다. 데이터가 하나라도 있으면 **`false`**, 아니면 **`true`**를 반환합니다. |
| **`void add(ItemType item)`** | 큐에 데이터를 추가합니다. |
| **`ItemType poll()`** | 큐에서 처음 추가된 데이터를 제거하고 반환합니다. |
| **`int front`** | 큐에서 마지막으로 poll한 데이터의 위치를 기록합니다. |
| **`int rear`** | 큐에서 가장 최근에 add한 데이터의 위치를 기록합니다. |
| **`ItemType data[maxsize]`** | 큐 데이터를 관리하는 배열입니다. 최대 **`maxsize`**개의 데이터를 저장할 수 있습니다. |

> 참고: 큐에서 데이터를 제거할 때, 메모리에서 데이터를 실제로 삭제하지 않고 front 포인터만 이동하여 다음 요소를 가리키도록 바뀝니다. 따라서 큐는 front의 다음 요소부터 rear까지의 데이터를 관리하는 구조라고 이해할 수 있습니다.
> 

---

## **큐의 동작 원리**

### 1. 큐에 요소를 추가(Enqueue)할 때

큐에 `10`, `20`, `30`을 순서대로 추가하는 경우를 가정합니다.

- **`front`**: 초기 상태에서 비어 있으며, 초기값은 `1` 또는 `0`으로 설정합니다.
- **`rear`**: 데이터가 추가되면서 마지막 요소를 가리키는 위치를 나타냅니다.

**큐 상태**:

```
[10, 20, 30]
 ^        ^
front    rear
```

---

### 2. 큐에서 요소를 제거(Dequeue)할 때

큐에서 `10`을 제거하면 **`front`** 포인터가 다음 요소(즉, `20`)를 가리키게 됩니다.

- 메모리에는 `10`이 남아 있을 수 있으나, 관리 대상에서 제외됩니다.

**큐 상태**:

```
[10, 20, 30]
      ^     ^
     front  rear

```

이제 **유효한 데이터는 `front`의 다음 요소(`20`)부터 `rear`까지**입니다.

---

## **자바에서 Queue 클래스 사용하기**

### **Queue 구현 예제**

```java
import java.util.ArrayDeque;
import java.util.Queue;

public class Main {
    public static void main(String[] args) {
        // Queue 객체 생성
        Queue<Integer> queue = new ArrayDeque<>();

        // 데이터 추가 (Enqueue)
        queue.add(10);
        queue.add(20);

        System.out.println("큐 크기: " + queue.size()); // 2

        // 큐가 비어 있는지 확인
        System.out.println("큐가 비었나요? " + queue.isEmpty()); // false

        // 큐에서 가장 먼저 추가된 값 확인 (Peek)
        System.out.println("가장 먼저 추가된 값: " + queue.peek()); // 10

        // 데이터 제거 (Dequeue)
        System.out.println("제거된 값: " + queue.poll()); // 10
        System.out.println("제거된 값: " + queue.poll()); // 20

        // 큐가 비어 있는지 확인
        System.out.println("큐가 비었나요? " + queue.isEmpty()); // true
    }
}
```

## 덱을 큐처럼 활용하기

덱(Double-Ended Queue)은 양쪽 끝에서 삽입과 삭제를 모두 지원합니다. 덱의 기능을 활용해 큐처럼 사용할 수도 있습니다.

### 덱을 활용한 큐 구현

```java
import java.util.ArrayDeque;

public class Main {
    public static void main(String[] args) {
        // ArrayDeque 객체 생성
        ArrayDeque<Integer> deque = new ArrayDeque<>();

        // 데이터 추가 (Enqueue)
        deque.addLast(10);
        deque.addLast(20);

        // 데이터 제거 (Dequeue)
        System.out.println(deque.pollFirst()); // 10
        System.out.println(deque.pollFirst()); // 20
    }
}
```

### **덱과 큐의 차이점**

- **큐(Queue):** 한쪽 끝에서 삽입(Enqueue)하고 반대쪽 끝에서 제거(Dequeue)하는 단방향 자료구조.
- **덱(Deque):** 양쪽 끝에서 삽입과 삭제가 가능한 자료구조.
