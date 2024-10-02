# List<Map<String, String>> 형식을 String[] 형식으로 변경하는 방법

Java에서 `List<Map<String, String>>` 형식을 `String[]` 형식으로 변경하는 방법에는 Stream API를 사용하는 방법과 전통적인 for 루프를 사용하는 방법이 있습니다.

## Stream API를 사용하는 방법

Stream API는 Java 8부터 도입된 기능으로, 컬렉션을 처리하는 데 있어 간결하고 선언적인 코딩 스타일을 제공합니다. 

```java
@Controller
public class SampleController{
    @Autowired
    private SampleService sampleService ;

    public void printHeaderTextArray() {
        // 서비스에서 데이터 가져오기
				List<Map<String, String>> headerList = sampleService.getHeaderList();

        // Stream API를 사용한 변환
        String[] headerTextArray = headerList.stream()
                                             .map(map -> map.get("HEADER_TEXT_LIST"))
                                             .toArray(String[]::new);

        // 결과 출력
        for (String header : headerTextArray) {
            System.out.println(header);
        }
        
        // 예제 데이터가 아래와 같을 경우:
        // headerList = [
        //     {"HEADER_TEXT_LIST": "1개월차", "SAVE_NAME_LIST": "M1"},
        //     {"HEADER_TEXT_LIST": "2개월차", "SAVE_NAME_LIST": "M2"},
        //     {"HEADER_TEXT_LIST": "3개월차", "SAVE_NAME_LIST": "M3"}
        // ]
        // 실제 출력 결과:
        // 1개월차
        // 2개월차
        // 3개월차
    }
}

```

## 전통적인 for 루프를 사용하는 방법

전통적인 for 루프를 사용하여 `List<Map<String, String>>` 형식을 `String[]` 형식으로 변환하는 방법도 있습니다. 이 방법은 모든 Java 버전에서 사용할 수 있으며, 코드가 명시적입니다.

```java
@Controller
public class SampleController {
    @Autowired
    private SampleService sampleService;

    public void printHeaderTextArray() {
        // 서비스에서 데이터 가져오기
        List<Map<String, String>> headerList = sampleService.getHeaderList();

        // 기존 for 루프를 사용한 변환
        List<String> headerTextList = new ArrayList<>();
        for (Map<String, String> map : headerList) {
            headerTextList.add(map.get("HEADER_TEXT_LIST"));
        }
        // 리스트를 배열로 변환
        String[] headerTextArray = new String[headerTextList.size()];
        headerTextArray = headerTextList.toArray(headerTextArray);

        // 결과 출력
        for (String header : headerTextArray) {
            System.out.println(header);
        }

        // 예제 데이터가 아래와 같을 경우:
        // headerList = [
        //     {"HEADER_TEXT_LIST": "1개월차", "SAVE_NAME_LIST": "M1"},
        //     {"HEADER_TEXT_LIST": "2개월차", "SAVE_NAME_LIST": "M2"},
        //     {"HEADER_TEXT_LIST": "3개월차", "SAVE_NAME_LIST": "M3"}
        // ]
        // 실제 출력 결과:
        // 1개월차
        // 2개월차
        // 3개월차
    }
}
```

## 각 방식의 장단점

### Stream API 방식

**장점**:

1. **간결성**: 코드가 더 짧고 읽기 쉽습니다.
2. **가독성**: 선언적인 스타일로 인해 데이터 처리 과정을 쉽게 이해할 수 있습니다.
3. **최신 기능**: 최신 Java 기능을 활용할 수 있습니다.

**단점**:

1. **학습 곡선**: Stream API에 익숙하지 않은 사람들에게는 다소 어려울 수 있습니다.
2. **성능**: 아주 큰 데이터셋의 경우, 성능이 떨어질 수 있습니다. (일반적으로는 미미한 차이)

### 전통적인 for 루프 방식

**장점**:

1. **명시성**: 각 단계가 명확히 표현되어 있어 이해하기 쉽습니다.
2. **호환성**: 모든 Java 버전에서 사용할 수 있습니다.
3. **성능**: 단순 반복 작업에서는 더 나은 성능을 보일 수 있습니다.

**단점**:

1. **장황함**: 코드가 길어지고 가독성이 떨어질 수 있습니다.
2. **실수 가능성**: 수동으로 변환하는 과정에서 실수가 발생할 가능성이 있습니다.

두 방법 중 어떤 것을 사용할지는 프로젝트의 요구사항이나 개인의 선호에 따라 달라질 수 있습니다. Stream API는 최신 Java 기능을 활용하여 코드를 간결하게 만들 수 있는 반면, 전통적인 for 루프는 모든 상황에서 사용할 수 있는 보편적인 방법입니다.
