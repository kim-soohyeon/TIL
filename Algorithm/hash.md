# **해시의 개념**

해시(hash)는 해시 함수를 사용하여 변환한 값을 인덱스로 활용해 **키와 값**을 저장하고, 빠르게 데이터를 탐색할 수 있는 자료구조입니다.

### 해시의 특징

1. **단방향성**
    
    키를 통해 값을 찾을 수 있지만, 값을 통해 키를 찾는 것은 불가능합니다.
    
2. **탐색 속도**
    
    평균적으로 O(1) 시간 복잡도로 데이터를 찾을 수 있습니다. 키를 해시 함수에 전달하면 값의 저장 위치를 바로 알 수 있으므로 별도의 탐색 과정이 필요 없습니다.
    
3. **해시 함수 필요**
    
    키를 효율적으로 인덱스로 변환하려면 적절한 해시 함수가 필요합니다.
    

### 해시의 활용 분야

- **비밀번호 관리**: 비밀번호를 직접 저장하지 않고, 해시 값을 저장하여 보안성을 강화.
- **데이터베이스 인덱싱**: 빠른 데이터 검색과 삽입을 지원.
- **블록체인**: 데이터 무결성을 유지하고, 보안성을 강화.

---

# 해시 함수

자바에서는 **HashSet**과 **HashMap**과 같은 표준 API를 제공하여 해시의 특성을 쉽게 활용할 수 있습니다.

### 자주 사용하는 해시 함수

1. **나눗셈법**
키를 특정 수로 나눈 나머지를 인덱스로 사용.
2. **곱셈법**
키에 특정 값을 곱한 후 소수점 이하 값을 인덱스로 변환.
3. **문자열 해싱**
문자열 키에 특화된 해시 함수로, 문자열 데이터를 효율적으로 처리.

# 충돌 처리

## **충돌(Collision)**

서로 다른 키가 동일한 해시 값을 가지는 상황.

## 충돌 처리 방법

### **1. 체이닝(Chaining)**

- 동일한 해시 값을 가진 데이터를 **Linked List**로 연결하여 저장.
- 자바의 **HashMap** 클래스는 체이닝 방식을 사용.
- **단점**
    - 메모리 사용량 증가.
    - 데이터가 많아질수록 탐색 속도가 느려질 수 있음.

### **2. 개방 주소법(Open Addressing)**

- 충돌 발생 시 빈 버킷을 찾아 데이터를 저장.
- 체이닝보다 메모리 효율이 높음.
- **개방 주소법의 종류**
    - **선형 탐사(Linear Probing)**
    충돌 발생 시 일정 간격으로 다음 빈 버킷 탐색.
    - **이중 해싱(Double Hashing)**
    해시 함수를 두 번 사용해 탐색 범위를 결정.

## **HashMap**

### **HashMap의 주요 메서드**

| 메서드 | 설명 |
| --- | --- |
| `put(KeyType key, ValueType value)` | 키와 값을 추가합니다. |
| `get(KeyType key)` | 키에 해당하는 값을 반환합니다. |
| `remove(KeyType key)` | 키와 해당 값을 삭제합니다. |
| `containsKey(KeyType key)` | 키의 존재 여부를 반환합니다. |
| `clear()` | 모든 데이터를 삭제합니다. |
| `isEmpty()` | 데이터가 비어 있는지 확인합니다. |
| `size()` | 저장된 데이터 개수를 반환합니다. |

### **HashMap 사용 예제**

```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        // HashMap 객체 생성
        HashMap<String, Integer> map = new HashMap<>();

        // 데이터 추가 (put)
        map.put("apple", 3);
        map.put("banana", 5);
        map.put("cherry", 7);

        // 데이터 조회 (get)
        System.out.println("apple의 개수: " + map.get("apple")); // 3

        // 데이터 삭제 (remove)
        map.remove("banana");

        // 키 존재 여부 확인 (containsKey
        System.out.println("banana가 있나요? " + map.containsKey("banana")); // false

        // 데이터 개수 확인 (size)
        System.out.println("현재 데이터 개수: " + map.size()); // 2

        // HashMap이 비어 있는지 확인 (isEmpty)
        System.out.println("HashMap이 비었나요? " + map.isEmpty()); // false

        // 모든 데이터 삭제 (clear)
        map.clear();
        System.out.println("HashMap이 비었나요? " + map.isEmpty()); // true
    }
}
```
