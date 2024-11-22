# 스택(Stack): 개념과 ADT 정의, 그리고 활용법 (Java 예제포함)

### 스택(Stack)
스택은 데이터를 ‘쌓는’ 구조로, 가장 나중에 입력된 데이터를 가장 먼저 꺼낼 수 있는 자료구조입니다. 이러한 동작 방식을 **후입선출** 또는 **LIFO(Last In First Out)**라고 합니다.

---


### **스택의 ADT(Abstract Data Type, 추상 자료형)**

| **메서드** | **설명** |
| --- | --- |
| **`boolean isFull()`** | 스택의 데이터 개수가 최대 크기(**`maxsize`**)인지 확인합니다. 가득 차 있다면 **`true`**, 아니면 **`false`** 를 반환합니다. |
| **`boolean isEmpty()`** | 스택에 데이터가 하나도 없는지 확인합니다. 데이터가 하나라도 있으면 **`false`**, 아니면 **`true`** 를 반환합니다. |
| **`void push(ItemType item)`** | 스택에 데이터를 추가합니다. |
| **`ItemType pop()`** | 스택에서 최근에 추가된 데이터를 제거하고 반환합니다. |
| **`int top`** | 스택에서 가장 최근에 추가된 데이터의 위치를 기록합니다. |
| **`ItemType data[maxsize]`** | 스택 데이터를 관리하는 배열입니다. 최대 **`maxsize`** 개의 데이터를 저장할 수 있습니다. |

---

# **Stack 클래스 사용하기**

```java
import java.util.Stack;

public class Main {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();// 스택 객체 생성
        
        // 데이터 푸시
        stack.push(10);
        stack.push(20);

        System.out.println(stack.size());// 2
        
        // 비어 있는지 확인
        System.out.println(stack.isEmpty());// false
        
        // 가장 최근 push한 값
        System.out.println(stack.peek());// 20
        
        // 데이터 팝
        System.out.println(stack.pop());// 20
        System.out.println(stack.pop());// 10
        
        // 비어 있는지 확인
        System.out.println(stack.isEmpty());// true
    }
}
```
